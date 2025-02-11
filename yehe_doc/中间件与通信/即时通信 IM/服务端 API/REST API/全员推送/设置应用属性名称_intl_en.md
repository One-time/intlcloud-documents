## Feature Description
Each app can set a maximum of 10 custom user attributes. This API is used to set the name of each attribute. After you set them, attribute names can be used for push by user attribute and other purposes.

## API Call Description
This feature **can only be applied for by Ultimate Edition users (but not by Pro Edition users). You can apply for this feature by submitting a ticket, and we will evaluate your needs for approval. If we determine that this feature suits your needs, we will approve your application so that you can use the feature**.

### Sample request URL
```
https://xxxxxx/v4/all_member_push/im_set_attr_name?usersig=xxx&identifier=admin&sdkappid=88888888&random=99999999&contenttype=json
```


### Request parameters

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https       | The request protocol is HTTPS, and the request method is POST.       |
| xxxxxx  | The country/region where your SDKAppID is located.<li>China:  `console.tim.qq.com `<li>Singapore:  `adminapisgp.im.qcloud.com `<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com` |
| v4/all_member_push/im_set_attr_name | Request API |
| usersig | The signature generated by the app admin account. For more information, see [UserSig backend API](https://intl.cloud.tencent.com/document/product/1047/34385). |
| identifier | It must be the app admin account. |
| sdkappid | The SDKAppID assigned by the IM console when the app is created. |
| random | A random 32-bit unsigned integer. |
| contenttype | Fixed value: JSON |

### Maximum call frequency

100 times/second

### Sample request packet
Set attribute 0 of the app to “sex”, attribute 1 to “city”, and attribute 2 to “country”.

```
{
	"AttrNames": {
		"0": "sex",
		"1": "city",
		"2": "country"
	}
}
```

### Request packet fields

| Field | Type | Required | Description |
|---------|---------|---------|-----|
| Digital key | String | Required | Indicates the specific attribute (“0” to “9”). |
| Attribute name | String | Required | The attribute name cannot exceed the length limit of 50 bytes. An app can have a maximum of 10 push attributes (numbered from 0 to 9), and users can customize the meaning of each attribute.

### Sample response packet

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0
}
```

### Response packet fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | The processing result of the request. OK: succeeded. FAIL: failed. |
| ErrorCode | Integer | Error code |
| ErrorInfo | String | Error information |

## Error Codes
The HTTP return code for this API is 200 unless a network error such as error 502 occurs. **The actual error code and error information are indicated by ErrorCode and ErrorInfo in the response packet.** For public error codes 60000 to 79999, see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The list below contains only error codes specific to this API:

| Error Code | Description |
|---------|---------|
| 90001 | Failed to parse the JSON format. Check whether the JSON request packet meets JSON specifications. |
| 90009 | The request requires the app admin’s permissions. |
| 91000 | An internal service error occurs. Please try again. |

## API Debugging Tool
To debug this API, you can use the [Online RESTful API Debugging Tool](https://29294-22989-29805-29810.cdn-go.cn/api-test.html#v4/all_member_push/im_set_attr_name).

## References
- [Push to all users APIs](https://intl.cloud.tencent.com/document/product/1047/37165) 
- [Push to all users](https://intl.cloud.tencent.com/document/product/1047/37166) 
- [Obtaining app attribute names](https://intl.cloud.tencent.com/document/product/1047/37168) 
- [Setting user attributes](https://intl.cloud.tencent.com/document/product/1047/37170)  
- [Deleting user attributes](https://intl.cloud.tencent.com/document/product/1047/37171)  
- [Obtaining user attributes](https://intl.cloud.tencent.com/document/product/1047/37169)  
- [Adding user tags](https://intl.cloud.tencent.com/document/product/1047/37173)  
- [Obtaining user tags](https://intl.cloud.tencent.com/document/product/1047/37172)  
- [Deleting user tags](https://intl.cloud.tencent.com/document/product/1047/37174)  
- [Deleting all user tags](https://intl.cloud.tencent.com/document/product/1047/37175)  
