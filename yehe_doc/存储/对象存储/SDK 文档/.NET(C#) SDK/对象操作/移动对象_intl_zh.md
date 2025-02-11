## 简介

本文档提供关于移动对象的相关的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名                       | 操作描述               |
| ------------------------------------------------------------ | ---------------------------- | ---------------------- |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | 设置对象复制（修改对象属性） | 复制文件到目标路径     |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | 删除单个对象                 | 在存储桶中删除指定对象 |

## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)。

## 移动对象

移动对象主要包括两个操作：复制源对象到目标位置，删除源对象。

由于 COS 通过存储桶名称（Bucket）和对象键（ObjectKey）来标识对象。移动对象也就意味着修改这个对象的标识，COS Java SDK 目前没有提供修改对象唯一标识名的单独接口，但是可以通过组合**复制对象**加上**删除对象**的基本操作，来达到修改对象标识的目的，从而实现移动对象。

例如将 mybucket-1250000000 这个存储桶中的 picture.jpg 这个对象移动到同个存储桶的 doc 路径下。首先可以复制 picture.jpg 对象到存储桶的 doc 路径下，即对象键设定为 doc/picture.jpg，复制完成后删除 picture.jpg 这个对象，来实现“移动”的效果。

同样的，如果想将 mybucket-1250000000 这个存储桶里的 picture.jpg 这个对象移动到 myanothorbucket-1250000000 这个存储桶里，可以先将对象复制到 myanothorbucket-1250000000 存储桶，然后删除原来的对象。



#### 示例代码

[//]: #	".cssg-snippet-move-object"

```cs
string sourceAppid = "1250000000"; //账号 appid
string sourceBucket = "sourcebucket-1250000000"; //"源对象所在的存储桶
string sourceRegion = "COS_REGION"; //源对象的存储桶所在的地域
string sourceKey = "sourceObject"; //源对象键
//构造源对象属性
CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, 
    sourceRegion, sourceKey);

// 存储桶名称，此处填入格式必须为 bucketname-APPID, 其中 APPID 获取参考 https://console.cloud.tencent.com/developer
string bucket = "examplebucket-1250000000";
string key = "exampleobject"; //目标对象的对象键

COSXMLCopyTask copyTask = new COSXMLCopyTask(bucket, key, copySource);

try {
  // 拷贝对象
  COSXML.Transfer.COSXMLCopyTask.CopyTaskResult result = await 
    transferManager.CopyAsync(copyTask);
  Console.WriteLine(result.GetResultInfo());

  // 删除对象
  DeleteObjectRequest request = new DeleteObjectRequest(sourceBucket, sourceKey);
  DeleteObjectResult deleteResult = cosXml.DeleteObject(request);
  // 打印结果
  Console.WriteLine(deleteResult.GetResultInfo());
} catch (Exception e) {
    Console.WriteLine("CosException: " + e);
}
```

> ?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MoveObject.cs) 查看。
