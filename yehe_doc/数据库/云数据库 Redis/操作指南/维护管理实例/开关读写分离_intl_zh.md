## 操作场景
云数据库 Redis 支持开启和关闭 [读写分离](https://intl.cloud.tencent.com/document/product/239/33132) 功能，针对读多写少的业务场景，解决热点数据集中的读需求，最大支持1主5从模式，提供最大5倍的读性能扩展能力。
>!
>- 开启读写分离，可能会导致数据读取不一致（副本节点数据延后于主节点），请先确认业务是否允许数据不一致的问题。
>- 关闭读写分离，可能会导致存量连接闪断，建议在业务低峰期进行操作。

## 操作步骤
1. 登录 [Redis 控制台](https://console.cloud.tencent.com/redis)， 在实例列表，单击实例 ID，进入实例管理页面。
2. 在实例管理页面，选择【节点管理】页，单击副本只读按钮，开启读写分离。
![](https://main.qcloudimg.com/raw/1d66625e3868fa6850648bd1737f7435.png)
3. 在弹出的对话框，确认信息无误后，单击【确定】即可。

