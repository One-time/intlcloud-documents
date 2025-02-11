## Feature Description
Through this API, the app admin can import groups without triggering callbacks or delivering notifications. When your app needs to be migrated to Instant Messaging (IM) from another instant messaging system, you can use this API to import existing group data.

## API Calling Description

### Applicable group types

| Group Type | Support This RESTful API |
|-----------|------------|
|Private|Yes, identical to Work in the new version|
|Public|Yes|
|ChatRoom|Yes, identical to Meeting in the new version|
|AVChatRoom|No|

IM provides the preceding five built-in group types. For details, see [Group Systems](https://intl.cloud.tencent.com/document/product/1047/33529).

> AVChatRoom and BChatRoom groups do not support importing basic group data. If you attempt to import basic group data for these types of groups, error 10007 returns. To achieve the effect of importing basic group data, you can [create a group](https://intl.cloud.tencent.com/document/product/1047/34895) and [modify basic group data](https://intl.cloud.tencent.com/document/product/1047/34962).


### Request URL example
```
https://xxxxxx/v4/group_open_http_svc/import_group?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```



### Request parameters
The following table lists and describes only the parameters to be modified when this API is called. For details on other parameters, see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https       | The request protocol is HTTPS, and the request method is POST.       |
| xxxxxx  | The country/region where your SDKAppID is located.<li>China:  `console.tim.qq.com `<li>Singapore:  `adminapisgp.im.qcloud.com `<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com` |
| v4/group_open_http_svc/import_group | The request API. |
| sdkappid | The SDKAppID assigned by the IM console when an app is created. |
| identifier | This must be the app admin account. For details, see [App Admins](https://intl.cloud.tencent.com/document/product/1047/33517#app-.E7.AE.A1.E7.90.86.E5.91.98). |
| usersig | The signature generated by the app admin account. For details, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | Enter a random 32-bit unsigned integer ranging from 0 to 4294967295. |

### Maximum calling frequency

The maximum calling frequency is 200 times per second.

### Request packet examples

- **Basic form**
Imports group data. In this example, the **CreateTime** parameter can be used to specify the group creation time.
```
{
    "Owner_Account": "leckie", // Group owner’s UserId (optional)
    "Type": "Public", // Group type, which can be Private, Public, or ChatRoom (required)
    "Name": "TestGroup", // Group name (required)
    "CreateTime": 1448357837 // Group creation time (optional). If this parameter is not specified, the default creation time is the request time.
}
```
- **Specifying other optional fields**
You can specify optional fields such as **Introduction** and **Notification**. The request format is the same as that of a group creation request. 
```
{
    "Owner_Account": "leckie", // Group owner’s UserId (optional)
    "Type": "Public", // Group type, which can be private, public, or ChatRoom (required)
    "GroupId":"MyFirstGroup", // User-defined group ID for external display (optional)
    "Name": "TestGroup", // Group name (required)
    "Introduction": "This is group Introduction", // Group introduction (optional)
    "Notification": "This is group Notification", // Group announcement (optional)
    "FaceUrl": "http://this.is.face.url",
    "MaxMemberCount": 500, // Maximum number of group members (optional)
    "ApplyJoinOption": "FreeAccess", // Method for handling group requests (optional)
    "CreateTime": 1448357837, // Group creation time (optional). If this parameter is not specified, the default creation time is the request time.
    "AppDefinedData": [ // Custom fields of the group (optional)
        {
            "Key": "GroupTestData1", // Key of the app custom field
            "Value": "xxxxx" // Value of the custom field
        },
        {
            "Key": " GroupTestData2",
            "Value": "abc\u0000\u0001" // Custom field supports binary data
        }
    ]
}
```


### Request packet fields

| Field | Type | Attribute | Description |
|---------|---------|---------|---------|
| Owner_Account | String | Optional | The group owner ID, which will be automatically added to group members. If this parameter is not specified, the group has no group owner. |
| Type | String | Required | The group type, which can be Public, Private, or ChatRoom. |
| GroupId | String | Optional | To simplify group IDs and make them memorable and propagable, Tencent Cloud allows apps to customize group IDs during group creation through RESTful APIs. For details, see [Group Systems](https://intl.cloud.tencent.com/document/product/1047/33529). |
| Name | String | Required | The group name with a maximum length of 30 bytes. |
| Introduction | String | Optional | Group introduction with a maximum length of 240 bytes. |
| Notification | String | Optional | The group announcement with a maximum length of 300 bytes. |
| FaceUrl | String | Optional | The URL of the group profile photo with a maximum length of 100 bytes. |
| MaxMemberCount | Integer | Optional | The maximum number of group members, which is 6,000 at the maximum. The default value is 2000. |
| ApplyJoinOption | String | Optional | The method for handling group requests, which are FreeAccess (no restriction), NeedPermission (approval required), and DisableApply (no entry). The default value is NeedPermission. |
| AppDefinedData | Array | Optional | The custom field of the group. By default, this field is unavailable and needs to be enabled before use. For details, see [Group Systems](https://intl.cloud.tencent.com/document/product/1047/33529). |
| CreateTime | Integer | Optional | The creation time of the group. |

### Response packet examples
- **Basic form**
```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0,
    "GroupId": "@TGS#2J4SZEAEL"
}
```

- **Specifying other optional fields**
```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0,
    "GroupId": "MyFirstGroup"
}
```


### Response packet fields

| Field | Type| Description |
|---------|---------|---------|
| ActionStatus | String | The request processing result. OK: succeeded. FAIL: failed. |
| ErrorCode | Integer | The error code. 0: succeeded. Other values: failed. |
| ErrorInfo | String | Error information. |
| GroupId | String | The resulting group ID from successful creation, which is assigned by the IM backend or specified by users. |

## Error Codes

Unless a network error (such as error 502) occurs, the HTTP return code for this API is always 200. ErrorCode and ErrorInfo in the response packet represent the actual error code and error information, respectively.
For common error codes (60000 to 79999), see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API.

| Error Code | Description |
|---------|---------|
| 10002 | An internal server error occurred. To correct it, try again. |
| 10003 | The request command word is invalid. |
| 10004 | A parameter is invalid. To correct it, check whether request parameters are correct based on the error description. |
| 10007 | Operation permissions are insufficient. For example, an ordinary member in a public group attempts to remove a member from the group, but only the app admin has the permission to do so. |
| 10021 | The group ID has been used. To correct it, use another group ID. |
| 80001 | Failed to pass text security filtering. To correct it, check whether the group name, group announcement, group introduction, or other contents contain sensitive words. |

## API Commissioning Tool

Use the [online commissioning tool for RESTful APIs](https://avc.cloud.tencent.com/im/APITester/APITester.html#group_open_http_svc/import_group) to commission this API.

## References

- Setting unread message counts for members ([v4/group_open_http_svc/set_unread_msg_num](https://intl.cloud.tencent.com/document/product/1047/34909))
- Importing a group member [v4/group_open_http_svc/import_group_member](https://intl.cloud.tencent.com/document/product/1047/34969))
- Dismissing a group ([v4/group_open_http_svc/destroy_group](https://intl.cloud.tencent.com/document/product/1047/34896))
