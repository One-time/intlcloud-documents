
本文为您介绍如何通过云数据库 MySQL 控制台设置数据库代理连接地址。

数据库代理访问地址独立于原有的数据库访问地址，通过数据库代理地址的请求全部通过代理集群中转访问数据库的主从节点，进行读写分离，将读请求转发至只读实例，降低主库的负载。

## 前提条件
已 [开通数据库代理](https://intl.cloud.tencent.com/document/product/236/42052)。

## 操作步骤
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，选择已开启代理的主实例，单击实例 ID 或**操作**列的**管理**，进入实例管理页面。
2. 在实例管理页面，选择**数据库代理**页，单击**数据库代理地址**后的<img src="https://main.qcloudimg.com/raw/be716b5360d5256a9d5e816e29872ec1.png"  style="margin:0;">图标。
![](https://main.qcloudimg.com/raw/63015c402bdd31e04e2597af84013a74.png)
3. 在弹出的对话框，修改代理地址后，单击**确定**。
>!修改内网地址会影响正在访问的数据库业务，建议在低峰期修改，请确保业务具备重连机制。
>
![](https://main.qcloudimg.com/raw/982fd53d880ab1a6d4f8df0372a99613.png)

