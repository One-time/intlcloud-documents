## Overview

This document provides an overview of APIs and SDK code samples related to persistent image processing.

| API | Description |
| :----------------------------------------------------------- | :----------------------------------- |
| [Persistent Image Processing](https://cloud.tencent.com/document/product/436/54050) | COS supports processing images upon upload. You can also process images that are already stored in COS and save the processed images to COS. |


## Processing upon Upload

#### Sample code

```php
try {
        $imageMogrTemplate = new Qcloud\Cos\ImageParamTemplate\ImageMogrTemplate(); //Create a parameter template instance for basic image processing
        $imageMogrTemplate->thumbnailByScale(50); //Scale an image to 50% of its original width and height
        $picOperationsTemplate = new \Qcloud\Cos\ImageParamTemplate\PicOperationsTemplate(); //Create a parameter template instance for persistent image processing
        $picOperationsTemplate->setIsPicInfo(1); //Set whether to return the input image information. `0`: no (default); `1`: yes
        $picOperationsTemplate->addRule($imageMogrTemplate, "resultobject"); //Set the image processing rule
        $result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID
        'Key' => 'exampleobject',
        'Body' => fopen('path/to/localFile', 'rb'), 
        'PicOperations' => $picOperationsTemplate->queryString(), //Generate parameters for presistent image processing
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Type | Description | Required |
| -------------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Uniquely identifies an object in a bucket. For example, if the object access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg`.  | Yes |
| Body | File/String | Uploaded content                                                   | Yes |
| PicOperations    | Json/String      | Persistent image processing information                                  | Yes       |


#### Response sample

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
    (
            [Body] =>
            [ETag] => "698d51a19d8a121ce581499d7b701668"
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [ContentLength] => 238186
            [Key] => exampleobject
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
            [Data] => Array
            (
                [OriginalInfo] => Array
                (
                    [Key] => exampleobject
                    [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
                    [ETag] => "7037fb6fb4cca43b958a28789605e73d98088720"
                    [ImageInfo] => Array
                    (
                            [Format] => JPEG
                            [Width] => 600
                            [Height] => 500
                            [Quality] => 90
                            [Ave] => 0x46442e
                            [Orientation] => 0
                     )

                )
                [ProcessResults] => Array
                (
                    [Object] => Array
                    (
                        [0] => Array(
                            [Key] => resultobject
                            [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/resultobject
                            [Format] => JPEG
                            [Width] => 300
                            [Height] => 200
                            [Size] => 30000
                            [Quality] => 90
                            [ETag] => "87c153bc2909aa0ba111ca126b675c510d36b817"
                        )
                    )
                )
            )
    )
)

```

#### Response description

| Parameter | Type | Description | Parent Node |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| Body                 | File/String | Response body                                    | None     |
| ETag | String | MD5 checksum of the file | None |
| RequestId             | String      | Request ID                                | None     |
| ContentLength | Int | Length of the response body | None |
| Key                  | String      | Object key                                    | None     |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| Location             | String      | Address of the requested resource                                 | None     |
| Data                 | Array      | Image processing result                              | None     |

## Processing In-Cloud Data

#### Sample code

```php
try {
        $imageMogrTemplate = new Qcloud\Cos\ImageParamTemplate\ImageMogrTemplate(); //Create an instance of the basic image processing parameter template
        $imageMogrTemplate->thumbnailByScale(50); //Scale an image to 50% of its original width and height
        $picOperationsTemplate = new \Qcloud\Cos\ImageParamTemplate\PicOperationsTemplate(); //Create a parameter template instance for persistent image processing
        $picOperationsTemplate->setIsPicInfo(1); //Set whether to return the input image information. `0`: no (default); `1`: yes
        $picOperationsTemplate->addRule($imageMogrTemplate, "resultobject"); //Set the image processing rule
        $result = $cosClient->ImageProcess(array(
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID
        'Key' => 'exampleobject',
        'PicOperations' => $picOperationsTemplate->queryString(), //Generate parameters for presistent image processing
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Type | Description | Required |
| -------------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Uniquely identifies an object in a bucket. For example, if the object access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg`.  | Yes |
| PicOperations    | Json/String      | Persistent image processing information                                  | Yes       |


#### Response sample

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
    (
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [Key] => exampleobject
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
            [OriginalInfo] => Array
            (
                [Key] => exampleobject
                [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
                [ETag] => "7037fb6fb4cca43b958a28789605e73d98088720"
                [ImageInfo] => Array
                (
                        [Format] => JPEG
                        [Width] => 600
                        [Height] => 500
                        [Quality] => 90
                        [Ave] => 0x46442e
                        [Orientation] => 0
                    )

            )
            [ProcessResults] => Array
            (
                [Object] => Array
                (
                    [0] => Array(
                        [Key] => resultobject
                        [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/resultobject
                        [Format] => JPEG
                        [Width] => 300
                        [Height] => 200
                        [Size] => 30000
                        [Quality] => 90
                        [ETag] => "87c153bc2909aa0ba111ca126b675c510d36b817"
                    )
                )
            )
    )
)

```

#### Response description

| Parameter | Type | Description | Parent Node |
| ------------------ | --------- | --------------------------------| ------ |
| RequestId             | String      | Request ID                                | None     |
| Key                  | String      | Object key                                    | None     |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| Location             | String      | Address of the requested resource                                 | None     |
| OriginalInfo         | Array      | Information of the input image                                    | None     |
| ProcessResults       | Array      | Image processing result                              |  None     |

