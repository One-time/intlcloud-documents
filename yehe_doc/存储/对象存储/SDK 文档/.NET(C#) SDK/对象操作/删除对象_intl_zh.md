## 简介

本文档提供关于对象的删除操作相关的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名       | 操作描述               |
| ------------------------------------------------------------ | ------------ | ---------------------- |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | 删除单个对象 | 在存储桶中删除指定对象 |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | 删除多个对象 | 在存储桶中批量删除对象 |

## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)。

## 删除单个对象

#### 功能说明

删除指定的对象（DELETE Object）。

#### 示例代码

[//]: #	".cssg-snippet-delete-object"

```cs
try
{
  // 存储桶名称，此处填入格式必须为 bucketname-APPID, 其中 APPID 获取参考 https://console.cloud.tencent.com/developer
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; //对象键
  DeleteObjectRequest request = new DeleteObjectRequest(bucket, key);
  //执行请求
  DeleteObjectResult result = cosXml.DeleteObject(request);
  //请求成功
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  //请求失败
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  //请求失败
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

> ?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/DeleteObject.cs) 查看。

## 删除多个对象

#### 功能说明

批量删除多个对象（DELETE Multiple Objects）。

#### 示例代码

[//]: #	".cssg-snippet-delete-multi-object"

```cs
try
{
  // 存储桶名称，此处填入格式必须为 bucketname-APPID, 其中 APPID 获取参考 https://console.cloud.tencent.com/developer
  string bucket = "examplebucket-1250000000";
  DeleteMultiObjectRequest request = new DeleteMultiObjectRequest(bucket);
  //设置返回结果形式
  request.SetDeleteQuiet(false);
  //对象key
  string key = "exampleobject"; //对象键
  List<string> objects = new List<string>();
  objects.Add(key);
  request.SetObjectKeys(objects);
  //执行请求
  DeleteMultiObjectResult result = cosXml.DeleteMultiObjects(request);
  //请求成功
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  //请求失败
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  //请求失败
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

> ?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/DeleteObject.cs) 查看。

## 指定前缀删除

#### 功能说明

指定前缀删除可以实现类似于删除目录的功能。

#### 示例代码

[//]: #	".cssg-snippet-delete-prefix"

```cs
try
{
  String nextMarker = null;

  // 循环请求直到没有下一页数据
  do
  {
    // 存储桶名称，此处填入格式必须为 bucketname-APPID, 其中 APPID 获取参考 https://console.cloud.tencent.com/developer
    string bucket = "examplebucket-1250000000";
    string prefix = "folder1/"; //指定前缀
    GetBucketRequest listRequest = new GetBucketRequest(bucket);
    //获取 folder1/ 下的所有对象以及子目录
    listRequest.SetPrefix(prefix);
    listRequest.SetMarker(nextMarker);
    //执行列出对象请求
    GetBucketResult listResult = cosXml.GetBucket(listRequest);
    ListBucket info = listResult.listBucket;
    // 对象列表
    List<ListBucket.Contents> objects = info.contentsList;
    // 下一页的下标
    nextMarker = info.nextMarker;
    
    DeleteMultiObjectRequest deleteRequest = new DeleteMultiObjectRequest(bucket);
    //设置返回结果形式
    deleteRequest.SetDeleteQuiet(false);
    //对象列表
    List<string> deleteObjects = new List<string>();
    foreach (var content in objects)
    {
      deleteObjects.Add(content.key);
    }
    deleteRequest.SetObjectKeys(deleteObjects);
    //执行批量删除请求
    DeleteMultiObjectResult deleteResult = cosXml.DeleteMultiObjects(deleteRequest);
    //打印请求结果
    Console.WriteLine(deleteResult.GetResultInfo());
  } while (nextMarker != null);
}
catch (COSXML.CosException.CosClientException clientEx)
{
  //请求失败
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  //请求失败
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

> ?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/DeleteObject.cs) 查看。
