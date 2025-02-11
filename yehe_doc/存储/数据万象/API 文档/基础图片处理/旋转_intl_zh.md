## 功能概述
腾讯云数据万象通过 **imageMogr2** 接口提供旋转功能，包括普通旋转和自适应旋转。

## 接口形式

```shell
download_url?imageMogr2/rotate/<rotateDegree>
					   /auto-orient
```

>请忽略上面的空格与换行符。


## 参数说明

| 参数                      | 含义                                                         |
| ------------------------- | ------------------------------------------------------------ |
| download_url | 文件的访问链接，具体构成为`<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`，<br>例如`examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`。 |
| /rotate/&lt;rotateDegree> | 普通旋转：图片顺时针旋转角度，取值范围0 - 360 ，默认不旋转。  |
| /auto-orient              | 自适应旋转：根据原图 EXIF 信息将图片自适应旋转回正。         |

## 示例

**普通旋转**
顺时针旋转90度，示例如下：

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/rotate/90
```

最终效果如下：
![](https://main.qcloudimg.com/raw/2d47c4f47b8f9c8eca85a3590a106e14.jpeg)
