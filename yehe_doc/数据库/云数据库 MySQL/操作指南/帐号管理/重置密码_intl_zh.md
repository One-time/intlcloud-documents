## 操作场景
云数据库 MySQL 支持重置实例密码，如您在使用云数据库 MySQL 过程中，忘记数据库账号密码或需修改密码，可通过控制台重新设置密码。
>?
>- 云数据库 MySQL 的重置密码功能已纳入 [CAM](https://intl.cloud.tencent.com/document/product/236/14469) 权限管理，建议对重置密码接口或云数据库 MySQL 实例敏感资源权限收紧，只授权给应该授权的人员。
>- 为了数据安全，建议您定期更换密码，最长间隔不超过3个月。


## 操作步骤
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb/)，在实例列表，单击实例 ID 或**操作**列的**管理**，进入实例管理页面。
2. 在实例管理页面，选择**数据库管理**>**帐号管理**页签，找到需要重置密码的帐号，选择**更多**>**重置密码**。
![](https://main.qcloudimg.com/raw/f8ff03d7b57ab9c96231f98920704441.png)
3. 在重置密码对话框，输入新密码和确认密码，单击**确定**。
>?数据库密码规格需要8 - 64个字符，至少包含英文、数字和符号 _+-&=!@#$%^*() 中的2种。
> 
![](https://main.qcloudimg.com/raw/8a2a4d08a1d14cfbcbb683f804bfeb78.png)

## 相关 API

| API 名称 | 描述 |
| ------------------------------------------------------------ | -------- |
| [ModifyAccountPassword](https://intl.cloud.tencent.com/document/product/236/17497) | 修改云数据库帐号的密码 |
