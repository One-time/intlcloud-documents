## Feature Description
 This API is used by the app admin to obtain the list of muted users in the group based on the group ID.

## API Calling Description
### Applicable group types

| Group Type ID | Is this RESTful API Supported? |
|-----------|------------|
| Private | Yes. Same as Work (work group for friends) in the new version. |
| Public | Yes. |
| ChatRoom | Yes. Same as Meeting (temporary meeting group) in the new version. |
| AVChatRoom | Yes. |
|Community| Yes.|

These are the 4 built-in group types in IM. For detailed information, see the [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).

#### Sample request URL
```
https://xxxxxx/v4/group_open_http_svc/get_group_shutted_uin?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```


### Request parameters

The list below contains only the parameters commonly used when calling this API and their descriptions. For more parameters, see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https       | The request protocol is HTTPS, and the request method is POST.       |
| xxxxxx  | The country/region where your SDKAppID is located.<li>China:  `console.tim.qq.com `<li>Singapore:  `adminapisgp.im.qcloud.com `<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com` |
| v4/group_open_http_svc/get_group_shutted_uin | Request API |
| sdkappid | SDKAppID assigned by the IM console when the application is created |
| identifier | The value must be the app admin account. For more information, see [App Admins](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | Signature generated by the app admin account. For details, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295 |

### Maximum calling frequency
The maximum calling frequency is 200 calls per second.
### Sample request packet

This is used to obtain the list of muted members in the group, and only the group ID is specified.
```
{
	 "GroupId":"@TGS#1KGZ2RAEU"
}
```

### Request packet fields

| Field | Type | Property | Description |
|---------|---------|---------|---------|
| GroupId | String | Required | ID of the group, in which the list of muted members needs to be obtained |

### Sample response packet body
```
{
    "ActionStatus": "OK",
    "ErrorCode": 0,
    "GroupId": "@TGS#2FZNNRAEU",
    "ShuttedUinList": [ // List of muted users in the group
        {
            "Member_Account": "tommy", // User ID
            "ShuttedUntil": 1458115189 // Expiration time (UTC time) of muting
        },
        {
            "Member_Account": "peter",
            "ShuttedUntil": 1458115189
        }
    ]
}
```

### Response packet fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | Result of the request. `OK` indicates that the request was successful, and `FAIL` indicates that the request failed. |
| ErrorCode | Integer | Error code. `0` indicates that the request was successful, and any non-zero value indicates that the request failed. |
| ErrorInfo | String | Detailed error information |
| ShuttedUinList | Array | The returned result is an array of muted users. The content includes the ID of each muted member and the expiration time (UTC time) of muting. |

## Error Codes

Unless a network error (such as error 502) occurs, the returned HTTP status code for this API is always 200. The specific error code and details can be found in the response packet fields such as `ErrorCode` and `ErrorInfo`.
For public error codes (60000 to 79999), see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The list below contains error codes specific to this API:

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 10002 | An internal server error occurred. Please try again. |
| 10003 | The request command word is invalid. |
| 10004 | A parameter is invalid. Check the error description and troubleshoot the issue. |
| 10007 | The operation permissions are insufficient. For example, to remove someone from a public group requires admin permissions. |
| 10010 | The group does not exist, or once existed but has been disbanded. |
| 10015 | The group ID is invalid. Be sure to use the correct group ID. |

## API Debugging Tool

Use the [online debugging tool for RESTful APIs](https://29294-22989-29805-29810.cdn-go.cn/api-test.html#v4/group_open_http_svc/get_group_shutted_uin) to debug this API.

## Reference
Batch muting and unmuting group members ([v4/group_open_http_svc/forbid_send_msg](https://intl.cloud.tencent.com/document/product/1047/34951))
