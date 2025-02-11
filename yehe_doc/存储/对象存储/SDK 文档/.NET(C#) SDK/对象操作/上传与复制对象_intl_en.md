## Overview

This document provides an overview of APIs and SDK sample codes related to uploading and replicating objects.


**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object | Uploads an object to a bucket. |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading an object using an HTML form | Uploads an object using an HTML form. |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object (modifying object attributes) | Copies a file to a destination path |
| [APPEND Object](https://intl.cloud.tencent.com/document/product/436/7741) | Appending parts  | Uploads an object by appending parts   |

**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart uploads. |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload operation | Initializes a multipart upload operation |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads an object in multiple parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying an object part | Copies a part of an object. |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a multipart upload. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of a file. |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload and deletes the uploaded parts. |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [Api Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Advanced APIs (Recommended)

### Uploading an object

#### Description


The advanced APIs encapsulate the simple upload and multipart upload APIs and can intelligently select the upload method based on file size. They also support checkpoint restart for resuming interrupted operations.

>?
> - If the file size is less than the multipart upload threshold, simple upload is used. Otherwise, multiple upload is used. The multipart upload threshold is configurable and is 5 MB by default.
> - The part size is configurable and is 1 MB by default.
> - If your .NET Framework version is 4.0 or earlier, advanced APIs are not available. For more information, please see Backward Compatibility.
> 

#### Sample code 1. Uploading a local file

[//]: # ".cssg-snippet-transfer-upload-file"
```cs
// Initialize TransferConfig.
TransferConfig transferConfig = new TransferConfig();

// Manually set the multipart upload threshold. If the object size is less than the threshold, simple upload is used. Otherwise, multipart upload is used. If no value is specified, the default value 5 MB is used.
transferConfig.DivisionForUpload = 5242880;
// Manually set the automatic part size for the advanced API. If no value is specified, the default value 1 MB is used.
transferConfig.SliceSizeForUpload = 2097152;

// Initialize TransferManager.
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket, formatted as `BucketName-APPID`
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
String srcPath = @"temp-source-file";// Absolute path to the local file

// Upload an object.
COSXMLUploadTask uploadTask = new COSXMLUploadTask(bucket, cosPath);
uploadTask.SetSrcPath(srcPath);

uploadTask.progressCallback = delegate (long completed, long total)
{
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
};

try {
  COSXML.Transfer.COSXMLUploadTask.UploadTaskResult result = await 
    transferManager.UploadAsync(uploadTask);
  Console.WriteLine(result.GetResultInfo());
  string eTag = result.eTag;
} catch (Exception e) {
    Console.WriteLine("CosException: " + e);
}
```

>?
> - For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferUploadObject.cs).
> - You can generate a download URL for the uploaded file using the same key. For detailed directions, please see [Generating a Pre-Signed Link](https://intl.cloud.tencent.com/document/product/436/37680). Please note that for private-read files, the download URL is only valid for a limited period of time.
>

#### Sample code 2. Uploading binary data

[//]: # ".cssg-snippet-transfer-upload-bytes"
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
  string cosPath = "exampleObject"; // Object key
  byte[] data = new byte[1024]; // Binary data
  PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, data);
  
  cosXml.PutObject(putObjectRequest);
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?
> - For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferUploadObject.cs).
> - You can generate a download URL for the uploaded file using the same key. For detailed directions, please see [Generating a Pre-Signed Link](https://intl.cloud.tencent.com/document/product/436/37680). Please note that for private-read files, the download URL is only valid for a limited period of time.
>

#### Sample code 3. Suspending, resuming, and canceling an upload

To suspend an upload, use the code below:

[//]: # ".cssg-snippet-transfer-upload-pause"
```cs
uploadTask.Pause();
```

To resume a suspended download, use the code below:

[//]: # ".cssg-snippet-transfer-upload-resume"
```cs
uploadTask.Resume();
```

To cancel an upload, use the code below:

[//]: # ".cssg-snippet-transfer-upload-cancel"
```cs
uploadTask.Cancel();
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferUploadObject.cs).
>

#### Sample code 4. Uploading multiple objects

[//]: # ".cssg-snippet-transfer-batch-upload-objects"
```cs
TransferConfig transferConfig = new TransferConfig();

// Initialize TransferManager.
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

string bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID

for (int i = 0; i < 5; i++) {
  // Upload an object.
  string cosPath = "exampleobject" + i; // Location identifier of the object in the bucket, i.e., the object key
  string srcPath = @"temp-source-file";// Absolute path to the local file
  COSXMLUploadTask uploadTask = new COSXMLUploadTask(bucket, cosPath); 
  uploadTask.SetSrcPath(srcPath);
  await transferManager.UploadAsync(uploadTask);
}
```

#### Sample code 5. Creating a directory

[//]: # ".cssg-snippet-create-directory"
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
  string cosPath = "dir/"; // Object key
  PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, new byte[0]);
  
  cosXml.PutObject(putObjectRequest);
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?
> - For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferUploadObject.cs).
> - You can generate a download URL for the uploaded file using the same key. For detailed directions, please see [Generating a Pre-Signed Link](https://intl.cloud.tencent.com/document/product/436/37680). Please note that for private-read files, the download URL is only valid for a limited period of time.
> 

### Copying objects

#### Description

The advanced APIs encapsulate async requests for the simple copy and multipart copy APIs and support pausing, resuming, and canceling copy requests.

>?
> - If the object size is less than the multipart copy threshold, simple copy is used. Otherwise, multiple copy is used. The multipart copy threshold is configurable and is 5 MB by default.
> - The part size is configurable and is 2 MB by default.
> 

#### Sample code

[//]: # ".cssg-snippet-transfer-copy-object"
```cs
// Initialize TransferConfig.
TransferConfig transferConfig = new TransferConfig();

// Manually set the multipart copy threshold. If the object size is less than the threshold, simple copy is used. Otherwise, multipart copy is used. If no value is specified, the default value 5 MB is used.
transferConfig.DivisionForCopy = 5242880;
// Manually set the automatic part size for the advanced API. If no value is specified, the default value 2 MB is used.
transferConfig.SliceSizeForCopy = 2097152;

// Initialize TransferManager.
TransferManager transferManager = new TransferManager(cosXml, transferConfig);

string sourceAppid = "1250000000"; // Account appid
string sourceBucket = "sourcebucket-1250000000"; //" Source object bucket
string sourceRegion = "COS_REGION"; // Source object bucket region
string sourceKey = "sourceObject"; // Source object key
// Construct the source object attributes
CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, 
    sourceRegion, sourceKey);

string bucket = "examplebucket-1250000000"; // Destination bucket in the format of BucketName-APPID
string key = "exampleobject"; // Object key of the destination bucket

COSXMLCopyTask copytask = new COSXMLCopyTask(bucket, key, copySource);

try {
  COSXML.Transfer.COSXMLCopyTask.CopyTaskResult result = await 
    transferManager.CopyAsync(copytask);
  Console.WriteLine(result.GetResultInfo());
  string eTag = result.eTag;
} catch (Exception e) {
    Console.WriteLine("CosException: " + e);
}
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/TransferCopyObject.cs).
>

## Simple Operations

### Uploading an object using simple upload

#### Description

This API (PUT Object) is used to upload an object smaller than 5 GB to a specified bucket. To call this API, you need to have permission to write the bucket. If the object size is larger than 5 GB, please use [Multipart Upload](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) or [Advanced APIs](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89) for the upload.

>!
> - The key (filename) cannot end with `/`; otherwise, it will be identified as a folder.
> - Each root account (`AAPID`) can have up to 1,000 bucket ACLs and an unlimited number of object ACLs. Do not configure ACLs for an object during upload if you don’t need to control access to it. The object will inherit the permissions of its bucket by default.
> 

#### Sample code

[//]: # ".cssg-snippet-put-object"
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
  string key = "exampleobject"; // Object key
  string srcPath = @"temp-source-file";// Absolute path to the local file

  PutObjectRequest request = new PutObjectRequest(bucket, key, srcPath);
  // Set the progress callback
  request.SetCosProgressCallback(delegate (long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  // Execute the request.
  PutObjectResult result = cosXml.PutObject(request);
  // Object Etag
  string eTag = result.eTag;
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?
> - For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/PutObject.cs).
> - You can generate a download URL for the uploaded file using the same key. For detailed directions, please see [Generating a Pre-Signed Link](https://intl.cloud.tencent.com/document/product/436/37680). Please note that for private-read files, the download URL is only valid for a limited period of time.
> 

### Uploading an object using an HTML form

#### Description

This API is used to upload an object using an HTML form.

#### Sample code

[//]: # ".cssg-snippet-post-object"
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
  string key = "exampleobject"; // Object key
  string srcPath = @"temp-source-file";// Absolute path to the local file
  PostObjectRequest request = new PostObjectRequest(bucket, key, srcPath);
  // Set the progress callback
  request.SetCosProgressCallback(delegate (long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  // Execute the request.
  PostObjectResult result = cosXml.PostObject(request);
  // Request successful
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/PostObject.cs).
>

### Copying an object (modifying object attributes)

#### Description

This API (PUT Object-Copy) is used to copy an object to a destination path.

#### Sample code 1: Copying an object with its attributes preserved

[//]: # ".cssg-snippet-copy-object"
```cs
try
{
  string sourceAppid = "1250000000"; // Account appid
  string sourceBucket = "sourcebucket-1250000000"; //" Source object bucket
  string sourceRegion = "COS_REGION"; // Source object bucket region
  string sourceKey = "sourceObject"; // Source object key
  // Construct the source object attributes
  CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, 
    sourceRegion, sourceKey);

  string bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
  string key = "exampleobject"; // Object key
  CopyObjectRequest request = new CopyObjectRequest(bucket, key);
  // Set the copy source
  request.SetCopySource(copySource);
  // Set whether to copy or update. Copy is used here.
  request.SetCopyMetaDataDirective(COSXML.Common.CosMetaDataDirective.Copy);
  // Execute the request.
  CopyObjectResult result = cosXml.CopyObject(request);
  // Request successful
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/CopyObject.cs).
>

#### Sample code 2: Copying an object while replacing its attributes

[//]: # ".cssg-snippet-copy-object-replaced"
```cs
try
{
  string sourceAppid = "1250000000"; // Account appid
  string sourceBucket = "sourcebucket-1250000000"; //" Source object bucket
  string sourceRegion = "COS_REGION"; // Source object bucket region
  string sourceKey = "sourceObject"; // Source object key
  // Construct the source object attributes
  CopySourceStruct copySource = new CopySourceStruct(sourceAppid, sourceBucket, 
    sourceRegion, sourceKey);

  string bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
  string key = "exampleobject"; // Object key
  CopyObjectRequest request = new CopyObjectRequest(bucket, key);
  // Set the copy source
  request.SetCopySource(copySource);
  // Set whether to copy or update. Copy is used here.
  request.SetCopyMetaDataDirective(COSXML.Common.CosMetaDataDirective.Replaced);
  // Replace metadata
  request.SetRequestHeader("Content-Disposition", "attachment; filename=example.jpg");
  // Execute the request.
  CopyObjectResult result = cosXml.CopyObject(request);
  // Request successful
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/CopyObject.cs).
>

#### Sample code 3: Modifying object metadata

[//]: # ".cssg-snippet-modify-object-metadata"
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
  string key = "exampleobject"; // Object key
  string appId = "1250000000"; // Account APPID
  string region = "COS_REGION"; // Region where the bucket of the source object resides
  // Construct object attributes
  CopySourceStruct copySource = new CopySourceStruct(appId, bucket, 
    region, key);

  CopyObjectRequest request = new CopyObjectRequest(bucket, key);
  // Set the copy source
  request.SetCopySource(copySource);
  // Set whether to copy or update. Copy is used here.
  request.SetCopyMetaDataDirective(COSXML.Common.CosMetaDataDirective.Replaced);
  // Replace metadata
  request.SetRequestHeader("Content-Disposition", "attachment; filename=example.jpg");
  request.SetRequestHeader("Content-Type", "image/png");
  // Execute the request.
  CopyObjectResult result = cosXml.CopyObject(request);
  // Request successful
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ModifyObjectProperty.cs).
>

#### Sample code 4: Modifying the storage class of an object

[//]: # ".cssg-snippet-modify-object-storage-class"
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
  string key = "exampleobject"; // Object key
  string appId = "1250000000"; // Account APPID
  string region = "COS_REGION"; // Region where the bucket of the source object resides
  // Construct object attributes
  CopySourceStruct copySource = new CopySourceStruct(appId, bucket, 
    region, key);

  CopyObjectRequest request = new CopyObjectRequest(bucket, key);
  // Set the copy source
  request.SetCopySource(copySource);
  // Set whether to copy or update. Copy is used here.
  request.SetCopyMetaDataDirective(COSXML.Common.CosMetaDataDirective.Replaced);
  // Change the storage class to ARCHIVE
  request.SetCosStorageClass("ARCHIVE");
  // Execute the request.
  CopyObjectResult result = cosXml.CopyObject(request);
  // Request successful
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ModifyObjectProperty.cs).


### Appending parts

#### Description

This API is used to upload an object by appending parts of the object.

#### Sample code

[//]: # ".cssg-snippet-append-object"
```cs
try
{
    string bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
    string key = "exampleobject"; // Object key
    string srcPath = @"temp-source-file";// Absolute path to the local file

    // Append the first part. 0 is passed in for the appending position, and an appendable object is created
    long next_append_position = 0;
    AppendObjectRequest request = new AppendObjectRequest(bucket, key, srcPath, next_append_position);
    // Set the progress callback
    request.SetCosProgressCallback(delegate (long completed, long total)
    {
        Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
    });
    AppendObjectResult result = cosXml.AppendObject(request);
    // Get the next appending position
    next_append_position = result.nextAppendPosition;
    Console.WriteLine(result.GetResultInfo());

    // Execute appending and pass in the object end obtained last time
    request = new AppendObjectRequest(bucket, key, srcPath, next_append_position);
    request.SetCosProgressCallback(delegate (long completed, long total)
    {
        Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
    });
    result = cosXml.AppendObject(request);
    Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
    // Request failed
    Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
    // Request failed
    Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/AppendObject.cs).

## Multipart Operations

The multipart upload process is outlined below.

#### Multipart upload/copy process

1. Initialize the multipart upload with `Initiate Multipart Upload` and get the `UploadId`.
2. Use the `UploadId` to upload parts with `Upload Part` or copy parts with `Upload Part Copy`
3. Complete the multipart upload with `Complete Multipart Upload`.

#### Resuming a multipart upload/copy operation

1. If you did not record the `UploadId` of the multipart upload, you can query the multipart upload job with `List Multipart Uploads` to get the `UploadId` of the corresponding file.
2. Use the `UploadId` to list the uploaded parts with `List Parts`.
3. Use the `UploadId` to upload the remaining parts with `Upload Part` or copy the remaining parts with `Upload Part Copy`.
4. Complete the multipart upload with `Complete Multipart Upload`.

#### Aborting a multipart upload/copy operation

1. If you did not record the `UploadId` of the multipart upload, you can query the multipart upload job with `List Multipart Uploads` to get the `UploadId` of the corresponding file.
2. Abort the multipart upload and delete the uploaded parts with `Abort Multipart Upload`.

### Querying multipart uploads

#### Description

This API (`List Multipart Uploads`) is used to query in-progress multipart uploads in a specified bucket.

#### Sample code

[//]: # ".cssg-snippet-list-multi-upload"
```cs
try
{
  String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
  ListMultiUploadsRequest request = new ListMultiUploadsRequest(bucket);
  // Execute the request.
  ListMultiUploadsResult result = cosXml.ListMultiUploads(request);
  // Request successful
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MultiPartsUploadObject.cs).
>

### Initializing a multipart upload

#### Description

This API is used to initialize a multipart upload operation and get its `uploadId`.

#### Sample code

[//]: # ".cssg-snippet-init-multi-upload"
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
  string key = "exampleobject"; // Object key
  InitMultipartUploadRequest request = new InitMultipartUploadRequest(bucket, key);
  // Execute the request.
  InitMultipartUploadResult result = cosXml.InitMultipartUpload(request);
  // Request successful
  this.uploadId = result.initMultipartUpload.uploadId; // The uploadId to use for subsequent multipart uploads
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MultiPartsUploadObject.cs).
>

### Uploading parts

#### Description

This API (`Upload Part`) is used to upload an object in parts.

#### Sample code

[//]: # ".cssg-snippet-upload-part"
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
  string key = "exampleobject"; // Object key
  string uploadId = "exampleUploadId"; // uploadId returned when the multipart upload is initialized
  int partNumber = 1; // Part number, increases incrementally starting from 1
  string srcPath = @"temp-source-file";// Absolute path to the local file
  UploadPartRequest request = new UploadPartRequest(bucket, key, partNumber, 
    uploadId, srcPath, 0, -1);
  // Set the progress callback
  request.SetCosProgressCallback(delegate (long completed, long total)
  {
    Console.WriteLine(String.Format("progress = {0:##.##}%", completed * 100.0 / total));
  });
  // Execute the request.
  UploadPartResult result = cosXml.UploadPart(request);
  // Request successful
  // Get the eTag of the returned part for subsequent CompleteMultiUploads.
  this.eTag = result.eTag;
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MultiPartsUploadObject.cs).
>

### Copying an object part

#### Description

This API is used to copy an object as a part.

#### Sample code

[//]: # ".cssg-snippet-upload-part-copy"
```cs
try
{
  string sourceAppid = "1250000000"; // Account appid
  string sourceBucket = "sourcebucket-1250000000"; //" Source object bucket
  string sourceRegion = "COS_REGION"; // Source object bucket region
  string sourceKey = "sourceObject"; // Source object key
  // Construct the source object attributes
  COSXML.Model.Tag.CopySourceStruct copySource = new CopySourceStruct(sourceAppid, 
    sourceBucket, sourceRegion, sourceKey);

  string bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
  string key = "exampleobject"; // Object key
  string uploadId = this.uploadId; // uploadId returned when the multipart upload is initialized
  int partNumber = 1; // Part number, increases incrementally starting from 1
  UploadPartCopyRequest request = new UploadPartCopyRequest(bucket, key, 
    partNumber, uploadId);
  // Set the copy source
  request.SetCopySource(copySource);
  // Set the range of parts to be copied, e.g., 0 to 1M
  request.SetCopyRange(0, 1024 * 1024);
  // Execute the request.
  UploadPartCopyResult result = cosXml.PartCopy(request);
  // Request successful
  // Get the eTag of the returned part for subsequent CompleteMultiUploads.
  this.eTag = result.copyPart.eTag;
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MultiPartsCopyObject.cs).
>

### Querying uploaded parts

#### Description

This API (`List Parts`) is used to query the uploaded parts of a multipart upload.

#### Sample code

[//]: # ".cssg-snippet-list-parts"
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
  string key = "exampleobject"; // Object key
  string uploadId = "exampleUploadId"; // uploadId returned when the multipart upload is initialized
  ListPartsRequest request = new ListPartsRequest(bucket, key, uploadId);
  // Execute the request.
  ListPartsResult result = cosXml.ListParts(request);
  // Request successful
  // List the parts that have been uploaded
  List<COSXML.Model.Tag.ListParts.Part> alreadyUploadParts = result.listParts.parts;
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MultiPartsUploadObject.cs).
>

### Completing a multipart upload

#### Description

This API (`Complete Multipart Upload`) is used to complete the multipart upload of a file.

#### Sample code
[//]: # ".cssg-snippet-complete-multi-upload"
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
  string key = "exampleobject"; // Object key
  string uploadId = "exampleUploadId"; // uploadId returned when the multipart upload is initialized
  CompleteMultipartUploadRequest request = new CompleteMultipartUploadRequest(bucket, 
    key, uploadId);
  // Concatenate uploaded parts in ascending order by partNumber.
  request.SetPartNumberAndETag(1, this.eTag);
  // Execute the request.
  CompleteMultipartUploadResult result = cosXml.CompleteMultiUpload(request);
  // Request successful
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/MultiPartsUploadObject.cs).
>

### Aborting a multipart upload

#### Description

This API (`Abort Multipart Upload`) is used to abort a multipart upload and delete the uploaded parts.

#### Sample code

[//]: # ".cssg-snippet-abort-multi-upload"
```cs
try
{
  string bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
  string key = "exampleobject"; // Object key
  string uploadId = "exampleUploadId"; // uploadId returned when the multipart upload is initialized
  AbortMultipartUploadRequest request = new AbortMultipartUploadRequest(bucket, key, uploadId);
  // Execute the request.
  AbortMultipartUploadResult result = cosXml.AbortMultiUpload(request);
  // Request successful
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  // Request failed
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  // Request failed
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/AbortMultiPartsUpload.cs).
>


