## 简介

本文档提供关于存储桶 Referer 白名单或者黑名单的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名         | 操作描述                   |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | 设置存储桶 Referer | 设置存储桶 Referer 白名单或者黑名单 |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | 查询存储桶 Referer | 查询存储桶 Referer 白名单或者黑名单 |

## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/)。

## 设置存储桶 Referer

#### 功能说明  

设置指定存储桶的 Referer 白名单或者黑名单（PUT Bucket referer）。

>! COS iOS SDK 版本需要大于等于 v5.9.6。
>

#### 请求示例
**Objective-C**

[//]: # ".cssg-snippet-put-bucket-referer"
```objective-c
QCloudPutBucketRefererRequest* request = [QCloudPutBucketRefererRequest new];

// 防盗链类型，枚举值：Black-List、White-List
request.refererType = QCloudBucketRefererTypeBlackList;

// 是否开启防盗链，枚举值：Enabled、Disabled
request.status = QCloudBucketRefererStatusEnabled;

// 是否允许空 Referer 访问，枚举值：Allow、Deny，默认值为 Deny
request.configuration = QCloudBucketRefererConfigurationDeny;

// 生效域名列表， 支持多个域名且为前缀匹配， 支持带端口的域名和 IP， 支持通配符*，做二级域名或多级域名的通配
request.domainList = @[@"*.com",@"*.qq.com"];

// 存储桶名称，格式为 BucketName-APPID
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError *error) {
    if (error){
        // 添加防盗链失败
    }else{
        // 添加防盗链失败
    }

}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketReferer:request];
```

>? 更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketReferer.m) 查看。
>

**Swift**

[//]: # ".cssg-snippet-put-bucket-referer"
```swift
let request = QCloudPutBucketRefererRequest.init();

// 防盗链类型，枚举值：Black-List、White-List
request.refererType = QCloudBucketRefererType.blackList;

// 是否开启防盗链，枚举值：Enabled、Disabled
request.status = QCloudBucketRefererStatus.enabled;

// 是否允许空 Referer 访问，枚举值：Allow、Deny，默认值为 Deny
request.configuration = QCloudBucketRefererConfiguration.allow;

// 生效域名列表， 支持多个域名且为前缀匹配， 支持带端口的域名和 IP， 支持通配符*，做二级域名或多级域名的通配
request.domainList = ["*.com","*.qq.com"];

// 存储桶名称，格式为 BucketName-APPID
request.bucket = "examplebucket-1250000000";

request.finishBlock = {(result,error) in
    if (error != nil){
        // 添加防盗链失败
    }else{
        // 添加防盗链失败
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketReferer(request);
```

>? 更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketReferer.swift) 查看。
>
## 查询存储桶 Referer

#### 功能说明

查询指定存储桶 Referer 白名单或者黑名单（GET Bucket referer）。

>! COS iOS SDK 版本需要大于等于 v5.9.6。
>


#### 请求示例
**Objective-C**

[//]: # ".cssg-snippet-get-bucket-referer"
```objective-c
QCloudGetBucketRefererRequest* request = [QCloudGetBucketRefererRequest new];

// 存储桶名称，格式为 BucketName-APPID
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(QCloudBucketRefererInfo * outputObject, NSError *error) {
    // outputObject 请求到的防盗链，详细字段请查看api文档或者SDK源码
    // QCloudBucketRefererInfo 类；
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketReferer:request];     
```
>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketReferer.m) 查看。

**Swift**

[//]: # ".cssg-snippet-get-bucket-referer"
```swift
let request = QCloudGetBucketRefererRequest.init();

// 存储桶名称，格式为 BucketName-APPID
request.bucket = "examplebucket-1250000000";

request.finishBlock = {(result,error) in
    // outputObject 请求到的防盗链，详细字段请查看api文档或者SDK源码
    // QCloudBucketRefererInfo 类；
}
QCloudCOSXMLService.defaultCOSXML().getBucketReferer(request);
```

>? 更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketReferer.swift) 查看。
>



