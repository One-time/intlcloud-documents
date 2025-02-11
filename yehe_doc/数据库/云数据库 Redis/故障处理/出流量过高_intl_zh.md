
## 现象描述
- 现象1：出流量指标达到上限。用户收到出流量限流触发告警的消息。
- 现象2：响应时延变大。

## 可能原因
主要可能原因如下：
- 由大 Key 引发。
- 实例配置不足。

## 解决思路
1. 在 Redis 控制台先调整实例的带宽，缓解当前的问题。
2. 之后查看并优化大 Key，优化方式有：
 - 拆分大 Key。
 - 在不影响业务的前提下，减少对大 Key 的访问。
 - 删除不必要的大 Key。
3. 优化后若仍存在带宽上限的问题，您可以对实例进行升级，增加实例的流量承载能力。 

## 处理步骤
### 步骤1：调整带宽
1. 登录 [Redis 控制台](https://console.cloud.tencent.com/redis)，在实例列表，单击实例 ID，进入实例详情页。
2. 在实例详情页的“网络信息”处，进行带宽调整，附加带宽的增加暂时不收费。
>?
>- 带宽增加不影响业务使用，降低带宽可能会导致流量超出带宽的流量被限制。
>- 标准带宽：实例中每个节点的带宽，节点类型包括主节点、副本节点。
>- 只读副本带宽：每个开启只读功能的副本，将拥有和主节点相同的带宽。
>- 附加带宽：标准带宽不满足需求的情况下，用户可自行新增的带宽。
>- 实例总带宽 = 附加带宽 * 分片数 + 标准带宽 * 分片数 * 副本数，标准架构的分片数=1，无副本的情况下可认为副本数=1。
>
![](https://main.qcloudimg.com/raw/00c7d78cc03dabf405ffff8fbc40eae5.png)

### 步骤2：优化大 Key
1. 登录 [Redis 控制台](https://console.cloud.tencent.com/redis)，在实例列表，单击实例 ID，进入实例管理页面。
2. 在实例管理页面选择【系统监控】页，查看 Key 大小分布，并优化大 Key。优化方式有：
 - 拆分大 Key。
 - 在不影响业务的前提下，减少对大 Key 的访问。
 - 删除不必要的大 Key。

若仍存在带宽上限问题，请执行 [步骤3：升级实例](#sjsl)。

### [步骤3：升级实例](id:sjsl)
#### 内存版（标准架构）升级
>!
>- 配置变更后，实例将按照新的规格计费。
>- 内存版（标准架构）扩容时，本机剩余容量不足以满足扩容需求，则会发生迁移，迁移过程中不影响业务访问，迁移完成后仅2.8版本会发生闪断，建议该版本业务侧有重连机制。
>- 因内存版（标准架构）最大容量为64GB，所以当内存版（标准架构）容量达到64GB时，无法再进行扩容。

1. 登录 [Redis 控制台](https://console.cloud.tencent.com/redis)，在实例列表，选中要升级的实例，在“操作”列选择【配置变更】>【扩容节点】或【增加副本】。
![](https://main.qcloudimg.com/raw/d4dbc95ee670595149c7609f03d8d92f.png)
2. 在弹出的配置变更对话框，选择需更改的配置，单击【确定】。
3. 返回实例列表，待实例状态变更为“运行中”，即可正常使用。

#### 内存版（集群架构）升级
>!
>- 配置变更后，实例将按照新的规格计费。
>- 新增分片操作，系统将自动均衡 Slot 配置，并且迁移数据。
>- 阻塞命令 BLPOP、BRPOP、BRPOPLPUSH、SUBSCRIBE 在扩缩容期间会存在1次或者多次命令失败（影响次数和分片数量相关），请在操作请评估好对业务的影响。
>

1. 登录 [Redis 控制台](https://console.cloud.tencent.com/redis)，在实例列表，选中要升级的实例，在“操作”列选择【配置变更】>【增加分片】、【扩容节点】或【增加副本】。
![](https://main.qcloudimg.com/raw/9c24103c52a67fbcd463e6f359ab0369.png)
2. 在弹出的配置变更对话框，选择需更改的配置，单击【确定】。
3. 返回实例列表，待实例状态变更为“运行中”，即可正常使用。

