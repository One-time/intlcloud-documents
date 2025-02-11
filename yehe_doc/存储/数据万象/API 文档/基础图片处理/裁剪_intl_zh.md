## 功能概述
腾讯云数据万象通过 **imageMogr2** 接口提供裁剪功能，包括普通裁剪、缩放裁剪、内切圆裁剪、圆角裁剪和人脸智能裁剪。

## 接口形式

```shell
download_url?imageMogr2/cut/<width>x<height>x<dx>x<dy>
                       /crop/<imageSizeAndOffsetGeometry>
                       /iradius/<radius>
                       /rradius/<radius>
                       /scrop/<Width>x<Height>
```

>请忽略上面的空格与换行符。


## 参数说明

| 参数         | 含义                                                         |
| ------------ | ------------------------------------------------------------ |
| download_url | 文件的访问链接，具体构成为`<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`，<br>例如`examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |

#### 普通裁剪参数说明

操作名称：cut。

| 参数        | 含义                                |
| ----------- | ----------------------------------- |
| &lt;width>  | 指定目标图片的宽为 width          |
| &lt;height> | 指定目标图片的高为 height          |
| &lt;dx>     | 相对于图片左上顶点水平向右偏移 dx |
| &lt;dy>     | 垂直向下偏移 dy                     |


>参数取值范围应大于0，小于原图宽高。


#### 缩放裁剪参数说明

操作名称：crop。

| 参数                         | 含义                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| /crop/&lt;Width>x            | 指定目标图片宽度为 Width ，高度不变。Width 取值范围应大于0，小于原图宽度 |
| /crop/x&lt;Height>           | 指定目标图片高度为 Height ，宽度不变。Height 取值范围应大于0，小于原图宽度 |
| /crop/&lt;Width>x&lt;Height> | 指定目标图片宽度为 Width，高度为 Height 。Width 和 Height 取值范围都应大于0，小于原图宽度 |

在进行缩放裁剪操作时，您也可以使用 gravity 参数指定操作的起点位置，详见下文中 [缩放裁剪操作示例](#缩放裁剪)。

<span id="1"></span>

#### 内切圆裁剪参数说明

操作名称：iradius。

| 参数                 | 含义                                                         |
| -------------------- | ------------------------------------------------------------ |
| /iradius/&lt;radius> | 内切圆裁剪功能，radius 是内切圆的半径，取值范围为大于0且小于原图最小边一半的整数。内切圆的圆心为图片的中心。图片格式为 gif 时，不支持该参数。 |

#### 圆角裁剪参数说明

操作名称：rradius。

| 参数                 | 含义                                                         |
| -------------------- | ------------------------------------------------------------ |
|/rradius/&lt;radius&gt;|  圆角裁剪功能，radius 为图片圆角边缘的半径，取值范围为大于0且小于原图最小边一半的整数。圆角与原图边缘相切。图片格式为 gif 时，不支持该参数。|



#### 人脸智能裁剪参数说明

操作名称：scrop。

| 参数                          | 含义                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| /scrop/&lt;Width>x&lt;Height> | 基于图片中的人脸位置进行缩放裁剪。目标图片的宽度为 Width、高度为 Height。 |

## 九宫格方位图

九宫格方位图可为图片的多种操作提供位置参考。红点为各区域位置的原点（通过 gravity 参数选定各区域后位移操作会以相应远点为参照）。 
![](https://main.qcloudimg.com/raw/53a143451229b4fbdd74935afe3832d5.png)

>
- 当 gravity 参数设置为 center 时，dx、dy 参数无效。
- 当 gravity 参数设置为 north 或 south 时，dx 参数无效（水印会水平居中）。
- 当 gravity 参数设置为 west 或 east 时，dy 参数无效（水印会垂直居中）。



## 示例

#### 普通裁剪

相对于图片左上顶点水平向右平移100像素，垂直向下平移10像素，指定目标图片大小为600×600进行裁剪：

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/cut/600x600x100x10
```

原图如下：
![](https://main.qcloudimg.com/raw/becc02d71fb703c2e87ad15e19808bb1.jpeg)

最终效果如下：
![](https://main.qcloudimg.com/raw/e28696af6be355cc678284b621a7c97b.jpeg)


<span id="缩放裁剪"></span>

#### 缩放裁剪

假设以中心点 center 为参考点，缩放裁剪至300×400，示例如下：

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/crop/300x400/gravity/center 
```

最终效果如下：
![](https://main.qcloudimg.com/raw/b9adeff300df483c22765b7d746d6690.jpeg)

#### 内切圆裁剪
取半径为300，进行内切圆裁剪：

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/iradius/300
```

最终效果如下：
![](https://main.qcloudimg.com/raw/f38ead869790236879a229f2d5f1bafc.jpeg)

#### 圆角裁剪
取半径为100，进行圆角裁剪：
```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/rradius/100 
```

最终效果如下：
![](https://main.qcloudimg.com/raw/795e0a3254137a5815b9f9f23cecbb91.jpeg)


#### 人脸智能裁剪
基于图片中的人脸位置进行缩放裁剪，目标图片大小为100×600，示例如下：

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/scrop/100x600
```

>如果图片中没有识别到人脸，则返回原图。
