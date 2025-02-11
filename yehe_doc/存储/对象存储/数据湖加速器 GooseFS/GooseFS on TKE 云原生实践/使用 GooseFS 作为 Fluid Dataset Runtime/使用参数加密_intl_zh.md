在 Fluid 中创建 Dataset 时，有时候我们需要在 `mounts` 中配置一些密钥信息，为了保证安全，Fluid 提供使用 Secret 来配置这些密钥信息的能力。

下面以访问 [对象存储（Cloud Object Storage，COS）](https://intl.cloud.tencent.com/product/cos) 数据集为例说明如何配置。

## 创建携带密钥信息的 Dataset

### 查看 Secret

在要创建的 Secret 中，需要写明在上面创建 Dataset 时需要配置的密钥信息。
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mysecret
stringData:
  fs.cosn.userinfo.secretId: <COS_ACCESS_KEY_ID>
  fs.cosn.userinfo.secretKey: <COS_ACCESS_KEY_SECRET>
```

可以看到，`fs.cosn.userinfo.secretKey` 和 `fs.cosn.userinfo.secretId` 的具体内容写在 Secret 中，Dataset 通过寻找配置中同名的 Secret 和 key 来读取对应的值，而不再是在 Dataset 直接写明，这样就保证了一些数据的安全性。

### 创建 Secret
```shell
$ kubectl apply -f secret.yaml 
secret/mysecret created

$ kubectl get secret
NAME        TYPE     DATA   AGE
mysecret   Opaque    2      57s
```

### 查看 Dataset 和 Runtime
```yaml
apiVersion: data.fluid.io/v1alpha1
kind: Dataset
metadata:
  name: mydata
spec:
  mounts:
    - mountPoint: cosn://<COS_BUCKET>/<COS_DIRECTORY>/
      name: mydata
      options:
        fs.cosn.bucket.region: <COS_REGION>
        fs.cosn.impl: org.apache.hadoop.fs.CosFileSystem
        fs.AbstractFileSystem.cosn.impl: org.apache.hadoop.fs.CosN
        fs.cos.app.id: <COS_APP_ID>
      encryptOptions:
        - name: fs.cosn.userinfo.secretId
          valueFrom:
            secretKeyRef:
              name: mysecret
              key: fs.cosn.userinfo.secretId
        - name: fs.cosn.userinfo.secretKey
          valueFrom:
            secretKeyRef:
              name: mysecret
              key: fs.cosn.userinfo.secretKey
---
apiVersion: data.fluid.io/v1alpha1
kind: GooseFSRuntime
metadata:
  name: mydata
spec:
  replicas: 1
  tieredstore:
    levels:
      - mediumtype: SSD
        path: /mnt/disk1/
        quota: 2G
        high: "0.8"
        low: "0.7"
```

可以看到，在上面的配置中，与直接配置 `fs.cos.endpoint` 不同，我们把 `fs.cosn.userinfo.secretId` 以及 `fs.cosn.userinfo.secretKey` 的配置改为从 Secret 中读取，以此来保障安全性。

>! 如果在 `options` 和 `encryptOptions` 中配置了同名的键，例如都有 `fs.cosn.userinfo.secretId` 的配置，那么 `encryptOptions` 中的值会覆盖 `options` 中对应的值的内容。
>

###  创建 Dataset 和 Runtime

```shell
$ kubectl create -f dataset.yaml
dataset.data.fluid.io/mydata created
goosefsruntime.data.fluid.io/mydata created
```

查看部署的 GooseFSRuntime 情况，显示都为 Ready 状态表示部署成功。

```shell
$ kubectl get goosefsruntime mydata
NAME     MASTER PHASE   WORKER PHASE   FUSE PHASE   AGE
mydata    Ready           Ready           Ready     62m
```

查看 dataset 的情况，现实 Bound 状态表示 dataset 绑定成功。

```shell
$ kubectl get dataset mydata
NAME     UFS TOTAL SIZE   CACHED   CACHE CAPACITY   CACHED PERCENTAGE   PHASE   AGE
mydata       210.00MiB       0.00B    2GiB              0.0%          Bound   1h
```

此时，使用 Secret 的 Dataset 即可获取到远程文件。

