## 操作场景
腾讯云容器镜像服务（Tencent Container Registry，TCR）企业版支持对托管的容器镜像进行安全扫描，生成扫描报告，暴露容器镜像内潜在的安全漏洞，并提供修复建议。容器镜像安全是云原生应用交付安全的重要一环，对上传的容器镜像进行及时安全扫描，并基于扫描结果选择阻断应用部署，可有效降低生产环境漏洞风险。

镜像安全扫描功能内置在镜像仓库中，用户可在上传容器镜像后，主动触发对指定版本容器镜像的安全扫描，也可以在命名空间层级配置自动扫描，该命名空间内新推送镜像上传完成后将自动被扫描。当前镜像安全扫描服务基于开源 Clair 方案，相关漏洞信息来自官方 CVE 漏洞库，并定期保持同步。

## 前提条件

在使用镜像安全扫描功能前，您需要完成以下准备工作：
- 已成功 [购买企业版实例](https://intl.cloud.tencent.com/document/product/1051/39088)。
- 如果使用子账号进行操作，请参考 [企业版授权方案示例](https://intl.cloud.tencent.com/document/product/1051/37248) 提前为子账号授予对应实例的操作权限。

## 操作步骤
### 配置扫描策略
1. 登录 [容器镜像服务](https://console.cloud.tencent.com/tcr) 控制台，选择左侧导航栏中的**命名空间**。
2. 在“命名空间”页面中，单击需开通镜像安全扫描功能的实例名称，进入命名空间详情页。
3. 在“基本信息”页，将安全扫描配置为**自动扫描**。如下图所示：
![](https://main.qcloudimg.com/raw/115b339d261ccceca8092829dc2fa390.png)

### 手动触发扫描
#### 步骤1：准备容器镜像
请参考 [镜像仓库基本操作](https://intl.cloud.tencent.com/document/product/1051/35488) 上传容器镜像，并在对应镜像仓库的版本管理页查看该镜像。
<span id="step2"></span>
#### 步骤2：触发镜像扫描
选择该镜像仓库内指定镜像版本，点击**扫描**触发镜像扫描，此时安全级别显示为“扫描中”。如下图所示：
![](https://main.qcloudimg.com/raw/0ffd1a76b8cca60faaec21bd37eee50e.png)


#### 步骤3：查看扫描结果
安全扫描完成后，安全级别处将自动展示当前镜像内漏洞的最高等级及个数，可单击查看漏洞详情。如下图所示：
![](https://main.qcloudimg.com/raw/0d5e243a57ea0130c975fa01fa0a62b0.png)
查看镜像的漏洞详情时，可单击指定的漏洞编号，跳转至该漏洞的详细说明，评估漏洞对业务的实际影响范围。如下图所示：
![](https://main.qcloudimg.com/raw/8170a2162576bed9b6e7d2d87d64929e.png)

#### 步骤4：重新触发扫描
因漏洞库会定时更新，您可参考 [步骤2：触发镜像扫描](#step2) 重新触发指定镜像的安全扫描，获取最新的扫描结果。
