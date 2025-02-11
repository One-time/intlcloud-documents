
## 简介

本文档提供关于对象标签的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名       | 操作描述                     |
| :----------------------------------------------------------- | :----------- | :--------------------------- |
| [PUT Object tagging](https://intl.cloud.tencent.com/document/product/436/35709) | 设置对象标签 | 为对象设置标签       |
| [GET Object tagging](https://intl.cloud.tencent.com/document/product/436/35710) | 查询对象标签 | 查询指定对象下已有的对象标签 |
| [DELETE Object tagging](https://intl.cloud.tencent.com/document/product/436/35711) | 删除对象标签 | 删除指定对象下已有的对象标签 |

## 设置对象标签

#### 功能说明

PUT Object tagging 用于为对象设置标签。


#### 方法原型

```
public Guzzle\Service\Resource\Model PutObjectTagging(array $args = array());
```

#### 请求示例


```php
try {
    $result = $cosClient->putObjectTagging(array(
        'Bucket' => 'examplebucket-1250000000', //格式：BucketName-APPID
        'Key'    => 'exampleobject',
        'TagSet' => array(
            array('Key'=>'key1',
                  'Value'=>'value1',
            ),  
            array('Key'=>'key2',
                  'Value'=>'value2',
            ),  
        ),  
    ));
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo "$e\n";
}
```

#### 参数说明

| 参数名称 | 描述                                                         | 类型   |
| -------- | ------------------------------------------------------------ | ------ |
| Bucket   | 设置标签的对象所在的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| Key      | 设置标签的对象键，对象键（Key）是对象在存储桶中的唯一标识，详情请参见 [对象键](https://intl.cloud.tencent.com/document/product/436/13324)  | String |
| TagSet    | 对象的标签配置集合                                                     | Array |

TagSet 成员说明：

|参数名称 | 描述 | 类型 |
| ----- | ---- | ---- |
| Key | 标签的 key | String |
| Value | 标签的 value | String |

## 查询对象标签

#### 功能说明

GET Object tagging 用于查询指定对象下已有的对象标签。

#### 方法原型

```
public Guzzle\Service\Resource\Model GetObjectTagging(array $args = array());
```

#### 请求示例

```php
try {
    $result = $cosClient->getObjectTagging(array(
        'Bucket' => 'examplebucket-1250000000', //格式：BucketName-APPID
        'Key'    => 'exampleobject',
    ));
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 参数说明

| 参数名称 | 描述                                                         | 类型   |
| -------- | ------------------------------------------------------------ | ------ |
| Bucket   | 设置标签的对象所在的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| Key      | 设置标签的对象键，对象键（Key）是对象在存储桶中的唯一标识，详情请参见 [对象键](https://intl.cloud.tencent.com/document/product/436/13324)  | String |



#### 返回结果示例

```php
GuzzleHttp\Command\Result Object
(
    [TagSet] => Array
        (
            [0] => Array
                (
                    [Key] => key1
                    [Value] => value1
                )

            [1] => Array
                (
                    [Key] => key2
                    [Value] => value2
                )

        )
    [RequestId] => NWRmMWVkMjFfMjJiMjU4NjRfNWQ3X2EwMWVj****
)
```

#### 返回结果说明

| 成员变量 | 描述     | 类型   |
| -------- | -------- | ------ |
| Key      | 标签的键 | String |
| Value    | 标签的值 | String |

## 删除对象标签

#### 功能说明

DELETE Object tagging 用于删除指定对象的已有标签。

#### 方法原型

```
public Guzzle\Service\Resource\Model DeleteObjectTagging(array $args = array());
```

#### 请求示例

```php
try {
    $result = $cosClient->deleteObjectTagging(array(
        'Bucket' => 'examplebucket-1250000000', //格式：BucketName-APPID
        'Key'    => 'exampleobject',
    );
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 参数说明

| 参数名称 | 描述                                                         | 类型   |
| -------- | ------------------------------------------------------------ | ------ |
| Bucket   | 设置标签的对象所在的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| Key      | 设置标签的对象键，对象键（Key）是对象在存储桶中的唯一标识，详情请参见 [对象键](https://intl.cloud.tencent.com/document/product/436/13324)  | String |


