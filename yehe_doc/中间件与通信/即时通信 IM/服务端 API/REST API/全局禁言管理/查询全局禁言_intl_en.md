## Background
- Global muting includes the global muting of one-to-one chat messages and that of group chat messages.
- By default, the global muting of one-to-one chat messages is disabled for accounts. If the global muting of one-to-one chat messages is enabled for an account, all one-to-one chat messages fail to be sent during the muting period. After the muting period expires, the IM backend system automatically disables the global muting of one-to-one chat messages, and then all one-to-one chat messages can be sent normally. For the permanent global muting of one-to-one chat messages, the muting period never expires.
- By default, the global muting of group chat messages is disabled for accounts. If the global muting of group chat messages is enabled for an account, all group chat messages fail to be sent during the muting period. After the muting period expires, the IM backend system automatically disables the global muting of group chat messages, and then all group chat messages can be sent normally. For the permanent global muting of group chat messages, the muting period never expires.

## Feature Description
- Query the account’s setting of global muting of one-to-one chat messages.
- Query the account’s setting of global muting of group chat messages.


## API Invocation Description

### Request URL example
```
https://xxxxxx/v4/openconfigsvr/getnospeaking?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```



### Request parameters

The following table lists and describes only the parameters to be modified when this API is invoked. For details on other parameters, see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https       | The request protocol is HTTPS, and the request method is POST.       |
| xxxxxx  | The country/region where your SDKAppID is located.<li>China:  `console.tim.qq.com `<li>Singapore:  `adminapisgp.im.qcloud.com `<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com` |
| v4/openconfigsvr/getnospeaking | The request API. |
| sdkappid | The SDKAppID assigned by the IM console when an app is created. |
| identifier | This must be the app admin account. For details, see [App Admins](https://intl.cloud.tencent.com/document/product/1047/33517#app-.E7.AE.A1.E7.90.86.E5.91.98). |
| usersig | The signature generated by the app admin account. For details, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | Enter a random 32-bit unsigned integer ranging from 0 to 4294967295. |


### Maximum invocation frequency

The maximum invocation frequency is 200 times per second.

### Request packet example

```
{
    "Get_Account": "lumotuwe"
}
```

### Request packet fields

| Field | Type | Attribute | Description |
|---------|---------|---------|---------|
| Get_Account | String | Required | Specify the account for which muting information is queried. |

### Response packet example

```
{
    "ErrorCode": 0,
    "ErrorInfo": "",
    "C2CmsgNospeakingTime": 4294967295,
    "GroupmsgNospeakingTime": 7196
}
```

### Response packet fields

| Field | Type | Description |
|---------|---------|---------|
| ErrorCode | Integer | The request error code. 0: succeeded. Others: failed. |
| ErrorInfo | String | Error information. |
| C2CmsgNospeakingTime | Number | The muting period for one-to-one chat messages, in seconds. The value is a non-negative integer. The 0 value indicates that message muting is disabled. The maximum value 4294967295 (or 0xFFFFFFFF in hexadecimal) indicates that permanent muting is enabled for the account. Other values indicate the specific muting period of the account. For example, the 3600 value indicates that the muting period of the account is 1 hour. |
| GroupmsgNospeakingTime | Number | The muting period for group chat messages, in seconds. The value is a non-negative integer. The 0 value indicates that message muting is disabled. The maximum value 4294967295 (or 0xFFFFFFFF in hexadecimal) indicates that permanent muting is enabled for the account. Other values indicate the specific muting period of the account. For example, the 3600 value indicates that the muting period of the account is 1 hour. |

## Error Codes
Unless a network error (such as error 502) occurs, the HTTP return code of this API is always 200. ErrorCode and ErrorInfo in the response packet represent the actual error code and error information, respectively.
For common error codes (60000 to 79999), see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API.

| Error Code | Description |
|---------|---------|
| 130001 | Failed to parse the JSON request packet. In this case, check whether the request packet meets JSON specifications. |
| 130002 | The JSON request packet does not include the Get_Account field. |
| 130003 | The Get_Account field in the JSON request packet is invalid. |
| 130014 | A JSON system error occurred. In this case, try again or contact our technical support service. |

## API Commissioning Tool

Use the [RESTful online commissioning tool for APIs](https://29294-22989-29805-29810.cdn-go.cn/api-test.html#v4/openconfigsvr/getnospeaking) to commission this API.

## References
Enabling global muting ([v4/openconfigsvr/setnospeaking](https://intl.cloud.tencent.com/document/product/1047/34923))
