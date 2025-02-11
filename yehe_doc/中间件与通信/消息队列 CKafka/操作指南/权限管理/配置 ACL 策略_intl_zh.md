## 操作场景

该任务指导您在使用消息队列 CKafka 时，通过控制台配置 SASL 鉴权和 ACL 规则，增强对公网/内网传输中的用户访问控制，增加对 Topic 等资源的生产消费权限控制。

>?
>- Kafka 提供了多种安全认证机制，主要分为 SSL 和 SASL2 大类，其中 SASL/PLAIN 是基于账号密码的认证方式，比较常用。CKafka 支持 SASL_PLAINTEXT 认证（参考  [添加路由策略-公网域名接入](https://intl.cloud.tencent.com/document/product/597/32555)）。
>- ACL 访问控制列表（Access Control List），帮助用户定义一组权限规则，允许/拒绝用户 user 通过 IP 读/写 Topic 资源。


## 操作步骤

### 配置 ACL 策略

1. 登录 [CKafka 控制台](https://console.cloud.tencent.com/ckafka) 。
2. 在顶部菜单栏，选择地域后，单击目标实例“ID/名称”。
3. 在实例详情页面，单击顶部**用户管理**页签。
4. 在用户管理页面，单击**新建**，填写用户名和密码信息，创建用户。
5. 单击顶部 **ACL策略管理**。
6. 在 ACL 策略详情页面，单击**批量配置**，为用户授予权限。

>?
>- 若只设置允许规则，则除允许的规则外的其他 IP 都无法连接实例。
>- 若只设置拒绝规则，则除拒绝的规则外的其他 IP 都可以连接实例。
>- 若同时设置允许规则和拒绝规则，则只有允许规则中的IP可以连接实例，其他 IP 都无法连接实例。 

<dx-tabs>
::: 2.4.1版本及以上实例
支持**批量勾选**和**按前缀模糊匹配**两种方式为用户授予权限。

- **批量勾选：**选择多个需要配置相同 ACL 策略的 Topic，批量勾选模式只支持配置一条策略。
- **按前缀模糊：**按 Topic 名称前缀模糊匹配需要配置相同 ACL 策略的 Topic，需要指定模糊匹配规则名称。设置后，新增按指定前缀命名的 Topic 时，系统自动配置指定 ACL 策略。

<dx-alert infotype="explain">
<ul>
<li>模糊匹配规则最多支持设置五条。</li>  
<li>支持输入多个IP或网段，用 `;` 隔开。</li>
</ul>
</dx-alert>

![](https://main.qcloudimg.com/raw/aab5317519ca8427e012aed9dcefde36.png)
:::
::: 其他版本实例
支持**批量勾选**为用户授予权限。

<dx-alert infotype="explain">
<ul>
<li>批量勾选模式只支持配置一条策略。</li> 
<li>支持输入多个IP或网段，用 `;` 隔开。</li> 
</ul>
</dx-alert>		

![](https://main.qcloudimg.com/raw/477c223aea0e0734bc7d56a2e233d5da.png)
:::
</dx-tabs>
    

### 使用限制

1. 开通路由只影响接入时的验证方式，设置的 ACL 权限则是全局的。

2. 如果您在开通公网访问路由的同时还使用了 PLAINTEXT 方式接入 CKafka，那么之前为 Topic 设置的 ACL 仍然会生效。若您希望 PLAINTEXT 方式的访问不受影响，请为 PLAINTEXT 需要访问的 Topic 添加全部用户的可读写的权限。
>?在添加ACL策略时，不需要选择任何用户，默认为**全部用户**添加了读写权限。
>
 ![](https://main.qcloudimg.com/raw/12e574cc76287026b4620c0802c6c08a.png)

   添加完成效果如下：
   ![](https://main.qcloudimg.com/raw/6d921dbdae519910c8f8b8eb3b5a89c7.png)

3. 如果该 Topic 已经在有其他云产品在使用（例如：日志服务 CLS 的日志投递、云函数 SCF 消息转储、大数据 EMR 组件的消费等），开启 ACL 策略相当于对这些联动能力的权限加以限制，会直接导致这些能力不可用，请一定谨慎操作。对于此类情况建议生产同一份数据到另一个 Topic 做分别处理，不要在同一个 Topic 上配置统一的 ACL 策略。

### 查看模糊匹配规则

1. 在 ACL 策略管理页面，选择**模糊匹配规则**。
2. 在模糊匹配规则列表，单击操作列的**详情**，可查看模糊匹配规则详情。

### 删除模糊匹配规则

1. 在 ACL 策略管理页面，选择**模糊匹配规则**。
2. 在模糊匹配规则列表，单击操作列的**删除**，可删除模糊匹配规则。

## 后续处理

完成授权后，用户可以通过 SASL 接入点接入消息队列 CKafka 并使用 PLAIN 机制消费消息（参考 [SDK 文档](https://intl.cloud.tencent.com/document/product/597/40049)）。
