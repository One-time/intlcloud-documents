
## 现象描述
- [现象1](id:xz1)：从 CVM 连接登录云数据库 Redis，连接失败。
- [现象2](id:xz2)：从数据库管理 DMC 平台连接登录云数据库 Redis，连接失败。

## 可能原因
- 网络问题。
- 安全组问题。
- 密码问题。
- 连接数已满。
- 内存写满或者分片写满。
- 需求访问外网但是无法访问。
- 发生HA切换、服务不可用、只读副本切换、只读副本服务不可用等。

## 解决思路
1. [使用 telnet 确认是 Redis 问题还是业务侧问题](#sytqr)。
2. [确认是否为密码问题](#qrsfwmmwt)。
3. [调整最大连接数](#tzzdljs)。
4. [确认是否内存写满或分片写满导致写入失败](#qrsfncxm)。
5. [通过 iptable 实现外网访问](#sxwwfw)。
6. [确认是否发生 HA 切换、服务不可用、只读副本切换、只读副本服务不可用等](#qrsffsh)。

## 处理步骤
### [使用 telnet 确认是 Redis 问题还是业务侧问题](id:sytqr)
大部分客户遇到的连接失败、无法连接等问题，一般为业务侧问题，可以通过命令行工具以及 telnet 缩小问题范围：
```js
[root@VM-4-10-centos ~]# telnet 10.x.x.34 6379
Trying 10.x.x.34...
Connected to 10.x.x.34.
Escape character is '^]'.
```
如上述所示，提示连接成功代表 Redis 实例没有问题，下面进行业务侧问题排查：

#### 1. 确认是否为网络问题
云服务器和数据库，须在同一账号同一个 VPC 内（保障同一个地域），或同在基础网络内，才能内网直接互通。
- 云服务器（CVM）采用私有网络（VPC），Redis 采用基础网络。建议将 Redis 从基础网络切换为 VPC 网络，请参见 [配置网络](https://intl.cloud.tencent.com/document/product/239/31944)。
- CVM 采用基础网络，Redis 采用 VPC。建议将 CVM 从基础网络切换为 VPC 网络，请参见 [切换私有网络服务](https://intl.cloud.tencent.com/document/product/213/20278)。
- CVM 与 Redis 在同一地域内，但属于不同的 VPC 网络。建议将 Redis 迁移到 CVM 所在的 VPC 网络，请参见 [配置网络](https://intl.cloud.tencent.com/document/product/239/31944)。
- CVM 与 Redis 不在同一地域内，属于不同的 VPC 网络。建议在两个 VPC 网络之间建立 [云联网](https://intl.cloud.tencent.com/zh/document/product/1003)。
- CVM 与 Redis 为不同账号，属于不同的 VPC 网络。建议在两个 VPC 网络之间建立 [云联网](https://intl.cloud.tencent.com/zh/document/product/1003)。

#### 2. 确认是否为安全组问题
若 CVM 和 Redis 的安全组配置有误，则会导致 CVM 无法连接 Redis。
-  [CVM 安全组配置有误](id:caqzpzyw)
若想使用 CVM 连接 Redis，需在 CVM 安全组中配置出站规则，**当出站规格的目标配置不为0.0.0.0/0且协议端口不为 ALL 时**，需要把 Redis 的 IP 及端口添加到出站规则中。
 1. 登录 [安全组控制台](https://console.cloud.tencent.com/cvm/securitygroup)，单击安全组名，进入 CVM 绑定的安全组详情页。
 2. 选择【出站规则】页，单击【添加规则】。
“类型”选择自定义；“目标”填写您 Redis 的 IP 地址（段）；“策略”选择允许。

- [Redis 安全组配置有误](id:maqzpzyw)
若想指定的 CVM 连接 Redis 实例，需要在 Redis 安全组中配置入站规则，**当入站规则的源端配置不为0.0.0.0/0且协议端口不为ALL时**，需要把 CVM 的 IP 及端口添加到入站规则中。 
 1. 登录 [安全组控制台](https://console.cloud.tencent.com/cvm/securitygroup)，单击安全组名，进入 Redis 绑定的安全组详情页。
 2. 选择【入站规则】页，单击【添加规则】。
填写您允许连接的 IP 地址（段）及需要放通的端口信息（Redis 内网端口），选择允许放通。
“类型”选择自定义；“来源”填写您 CVM 的 IP 地址（段）；“策略”选择允许。
>!  
>- Redis 内网默认端口为6379，同时支持自定义端口，若修改过默认端口号，安全组中需放通 Redis 新端口信息。
>- 安全组入站规则需要放通 Redis 实例的6379端口。

### [确认是否为密码问题](id:qrsfwmmwt)
执行 info 命令进行测试，如果执行提示如下，说明 Redis 密码没有问题。
```js
[root@SNG-Qcloud /data/home/rickyu]# redis-cli -h 10.x.x.34 -p 6379 -a password
10.x.x.2:6379> info cpu
# CPU
used_cpu_sys:1623.176000
used_cpu_user:4649.572000
used_cpu_sys_children:0.000000
used_cpu_user_children:0.000000
```
如果执行提示`NOAUTH Authentication required.`代表密码错误。
```js
10.0.4.31:6379> info memory
NOAUTH Authentication required.
10.0.4.31:6379> 
```
#### 解决方案
登录 [Redis 控制台](https://console.cloud.tencent.com/redis)，单击实例 ID 进入详情页，进行密码重置即可，详情请参见 [管理账号](https://intl.cloud.tencent.com/document/product/239/34590)。
![](https://qcloudimg.tencent-cloud.cn/raw/fe7308090ce478150a0b1c5706bc1aef.png)

### [调整最大连接数](id:tzzdljs)
1. 登录 [Redis 控制台](https://console.cloud.tencent.com/redis)，单击实例 ID，进入实例详情页。
2. 在详情页的“最大连接数”处，单击【调整】可修改最大连接数。
>?用户可在控制台修改 Proxy 的最大连接数，如需修改 Redis 的最大连接数，请 [提交工单](https://console.cloud.tencent.com/workorder/category) 获取帮助。
>
![](https://qcloudimg.tencent-cloud.cn/raw/40d1e79d20b29d4f381f53d79ecd9144.png)
3. 在系统监控页，选择【连接使用率】指标，可查看连接使用率。
Proxy 监控：
![](https://qcloudimg.tencent-cloud.cn/raw/ba5071d61ba24b97e1bc69b2d28e48d3.png)
Redis 监控：
![](https://qcloudimg.tencent-cloud.cn/raw/38dc0b1facdff97aec660e4c54e0b9d5.png)

### [确认是否内存写满或分片写满导致写入失败](id:qrsfncxm)
如果业务报错：
```js
"-READONLY You can't write against a read only slave.\r\n"
```
登录 [Redis 控制台](https://console.cloud.tencent.com/redis)，单击实例 ID 进入系统监控页面，查看监控发现内存写满情况：
![](https://qcloudimg.tencent-cloud.cn/raw/7a63fbc80e9cb39c317b842d458866cf.png)
内存写满情况下，写入失败，需要立即进行 [扩容](https://intl.cloud.tencent.com/document/product/239/31934) 或者将驱逐策略调整为`allkeys-lru`或者`volatile-lru`。

>?驱逐策略调整为`allkeys-lru`，会对业务数据有损，请根据实际需求评估。

### [通过 iptable 实现外网访问](id:sxwwfw)
云数据库 Redis 暂时不支持外网访问，您可以通过具备外网 IP 的云服务器 CVM 进行端口转发，来实现外网访问 Redis 实例，请参见 [iptable 转发](https://intl.cloud.tencent.com/document/product/239/35905) 。
>?iptable 转发的方式存在稳定性风险，不建议在生产环境使用外网接入。


### [确认是否发生 HA 切换、服务不可用、只读副本切换、只读副本服务不可用等](id:qrsffsh)
如果在某个确定的时间点发现连接异常或者有大量的访问报错，慢查询，同时接受到云监控事件告警，代表发生了异常事件。

**[云监控](https://console.cloud.tencent.com/monitor/alarm2/policy) 事件告警配置方法**：
![](https://qcloudimg.tencent-cloud.cn/raw/f7de41a133dd54b2c82574f2bbbc1dde.png)

## 附录
### [网络类型/ VPC 判断方法](id:wllxvpdff)
使用内网地址连接云数据库时，CVM 和 Redis 须是同一账号，且同一个 VPC 内（保障同一个地域），或同在基础网络。
>?
>- 如果实例列表的“网络”处，均显示为“基础网络”或均显示为“VPC”，则表示 CVM 和 Redis 是同一网络类型。
>- 如果实例列表的“网络”处，均显示为同一个“VPC”（保障同一个地域），则表示 CVM 和 Redis 是同一 VPC。
>
- **查看 CVM 网络类型/同一 VPC** ：登录 [CVM 控制台](https://console.cloud.tencent.com/cvm/instance)，在实例列表查看“网络”。
![](https://qcloudimg.tencent-cloud.cn/raw/ad8661c3906fa96962618e51b731fc4d.png)
- **查看 Redis 网络类型/同一 VPC**：登录 [Redis 控制台](https://console.cloud.tencent.com/redis)，在实例列表查看“网络”。
![](https://qcloudimg.tencent-cloud.cn/raw/920e151463fc3f6087c671294b05ee46.png)
