## 简介

本文档提供关于对象标签的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名       | 操作描述                     |
| :----------------------------------------------------------- | :----------- | :--------------------------- |
| [PUT Object tagging](https://intl.cloud.tencent.com/document/product/436/35709) | 设置对象标签 | 为已上传的对象设置标签       |
| [GET Object tagging](https://intl.cloud.tencent.com/document/product/436/35710) | 查询对象标签 | 查询指定对象下已有的对象标签 |
| [DELETE Object tagging](https://intl.cloud.tencent.com/document/product/436/35711) | 删除对象标签 | 删除指定对象下已有的对象标签 |


## 设置对象标签

#### 功能说明

COS 支持为已存在的对象设置标签。PUT Object tagging 接口通过为对象添加键值对作为对象标签，可以协助您分组管理已有的对象资源，详情请参见 [对象标签概述](https://intl.cloud.tencent.com/document/product/436/35665)。

#### 方法原型

```go
func (s *ObjectService) PutTagging(ctx context.Context, name string, opt *ObjectPutTaggingOptions, id ...string) (*Response, error)
```

#### 请求示例

[//]: # (.cssg-snippet-put-object-tagging)
```go
// Case1 通过 PutTagging 设置云上对象标签
opt := &cos.ObjectPutTaggingOptions{
    TagSet: []cos.ObjectTaggingTag{
        {
            Key:   "test_k2",
            Value: "test_v2",
        },
        {
            Key:   "test_k3",
            Value: "test_v3",
        },
    },
}
name := "example"
_, err := c.Object.PutTagging(context.Background(), name, opt)
if err != nil {
    //ERROR
}

// Case2 上传时设置对象标签
name = "test/example"
f := strings.NewReader("test")
popt := &cos.ObjectPutOptions{
    ObjectPutHeaderOptions: &cos.ObjectPutHeaderOptions{
        XOptionHeader: &http.Header{},
    },
}
popt.XOptionHeader.Add("x-cos-tagging", "Key1=Value1&Key2=Value2")
_, err = c.Object.Put(context.Background(), name, f, popt)
```

#### 参数说明

```go
type ObjectPutTaggingOptions struct {
    TagSet  []ObjectTaggingTag
}
type BucketTaggingTag struct {
    Key   string
    Value string
}
```
| 参数名称 | 参数描述                                                     | 类型   | 是否必填 |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| name     | 对象键（Key）是对象在存储桶中的唯一标识。例如，在对象的访问域名 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg` 中，对象键为 doc/pic.jpg | String | 是   |
| TagSet   | 标签集合，最多支持10个标签    | Array  | 是   |
| Key      | 标签键，长度不超过128字节，支持英文字母、数字、空格、加号、减号、下划线、等号、点号、冒号、斜线 | String | 是   |
| Value    | 标签值，长度不超过256字节，支持英文字母、数字、空格、加号、减号、下划线、等号、点号、冒号、斜线 | String | 是   |

## 查询对象标签

#### 功能说明

GET Object tagging 接口用于查询指定对象下已有的对象标签。

#### 方法原型

```go
func (s *ObjectService) GetTagging(ctx context.Context, name string, id ...string) (*ObjectGetTaggingResult, *Response, error)
```

#### 请求示例

[//]: # (.cssg-snippet-get-object-tagging)
```go
name := "example"
res, _, err := c.Object.GetTagging(context.Background(), name)
if err != nil {
    //ERROR
}
```

#### 结果说明
```go
type ObjectGetTaggingResult struct {
    TagSet  []ObjectTaggingTag
}
type BucketTaggingTag struct {
    Key   string
    Value string
}
```

| 参数名称 | 参数描述                                                     | 类型   |
| -------- | ------------------------------------------------------------ | ------ |
| TagSet   | 标签集合，最多支持10个标签    | Array  |
| Key      | 标签键，长度不超过128字节，支持英文字母、数字、空格、加号、减号、下划线、等号、点号、冒号、斜线 | String |
| Value    | 标签值，长度不超过256字节，支持英文字母、数字、空格、加号、减号、下划线、等号、点号、冒号、斜线 | String |

## 删除对象标签

#### 功能说明

DELETE Object tagging 接口用于删除指定对象下已有的对象标签。

#### 方法原型

```go
func (s *ObjectService) DeleteTagging(ctx context.Context, name string, id ...string) (*Response, error)
```

#### 请求示例

[//]: # (.cssg-snippet-delete-object-tagging)
```go
name := "example"
_, err = c.Object.DeleteTagging(context.Background(), name)
if err != nil {
    //ERROR
}
```
