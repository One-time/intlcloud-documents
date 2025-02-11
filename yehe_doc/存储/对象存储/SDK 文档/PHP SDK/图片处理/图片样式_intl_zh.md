
## 简介

本文档提供关于图片样式相关的 API 概览以及 SDK 示例代码。

| API                                                          | 说明       |
| :----------------------------------------------------------- | :--------- |
| [增加样式](https://intl.cloud.tencent.com/document/product/1045/33708)  | 增加存储桶样式  |
|  [查询样式](https://intl.cloud.tencent.com/document/product/1045/33707)  | 查询存储桶样式       |
|  [删除样式](https://intl.cloud.tencent.com/document/product/1045/33709)   |  删除存储桶样式 |


## 增加样式

#### 功能说明

对某一个存储桶设置样式功能，后续上传到该存储桶的图片文件都会被添加指定的样式。

#### 示例代码

```php
try {
        $result = $cosClient->PutBucketImageStyle(array(
        'Bucket' => 'examplebucket-1250000000', //格式：BucketName-APPID
        'StyleName' => 'style_name',//样式名称
        'StyleBody' => 'imageMogr2/thumbnail/!50px', //样式信息
    ));
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 参数说明

| 参数名称             | 类型        | 描述                                                         | 是否必填 |
| -------------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket          | String      | 存储桶名称，格式：BucketName-APPID                        | 是       |
| StyleName          | String      | 样式名称                        | 是       |
| StyleBody          | String      | 样式信息                        | 是       |


#### 返回结果示例

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.pic.ap-beijing.myqcloud.com/
        )
)

```

#### 返回结果说明

| 参数名称             | 类型        | 描述                                          | 父节点  |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| RequestId             | String      | 请求 ID 标识                                | 无     |
| Bucket               | String      | 存储桶名称，格式：BucketName-APPID              | 无     |
| Location             | String      | 请求资源地址                                 | 无     |

## 查询样式

#### 功能说明

查询某个存储桶下已有的样式。

#### 示例代码
```php
try {
        $result = $cosClient->GetBucketImageStyle(array(
        'Bucket' => 'examplebucket-1250000000', //格式：BucketName-APPID
        'StyleName' => 'style_name', //样式名称
    ));
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 参数说明

| 参数名称             | 类型        | 描述                                                         | 是否必填 |
| -------------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket          | String      | 存储桶名称，格式：BucketName-APPID                        | 是       |
| StyleName       | String      | 样式名称                                               | 否       |


#### 返回结果示例

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.pic.ap-beijing.myqcloud.com/
            [StyleRule] => Array(
                [0] => Array(
                    [StyleName] => style_name
                    [StyleBody] => imageMogr2/thumbnail/!50px
                )
            )
       )
)

```

#### 返回结果说明

| 参数名称             | 类型        | 描述                                          | 父节点  |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| RequestId             | String      | 请求 ID 标识                                | 无     |
| Bucket               | String      | 存储桶名称，格式：BucketName-APPID              | 无     |
| Location             | String      | 请求资源地址                                 | 无     |
| StyleRule             | Array      | 样式信息列表                                 | 无     |

## 删除样式

#### 功能说明

删除某一特定样式。

#### 示例代码
```php
try {
        $result = $cosClient->DeleteBucketImageStyle(array(
        'Bucket' => 'examplebucket-1250000000', //格式：BucketName-APPID
        'StyleName' => 'style_name', //样式名称
    ));
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 参数说明

| 参数名称             | 类型        | 描述                                                         | 是否必填 |
| -------------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket          | String      | 存储桶名称，格式：BucketName-APPID                        | 是       |
| StyleName       | String      | 样式名称                                               | 是       |


#### 返回结果示例

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.pic.ap-beijing.myqcloud.com/
       )
)

```

#### 返回结果说明

| 参数名称             | 类型        | 描述                                          | 父节点  |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| RequestId             | String      | 请求 ID 标识                                | 无     |
| Bucket               | String      | 存储桶名称，格式：BucketName-APPID              | 无     |
| Location             | String      | 请求资源地址                                 | 无     |

