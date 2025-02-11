数据库实例是在腾讯云中独立运行的数据库环境。一个数据库实例可以包含多个由用户创建的数据库，并且可以使用与独立数据库实例相同的工具和应用程序进行访问。

腾讯云数据库 MySQL 有如下两种数据库实例：

<table>
<thead><tr>
<th>实例类型</th><th width="20%">定义</th><th width="15%">架构</th><th>实例列表是否可见</th><th>功能</th></tr></thead>
<tbody><tr>
<td>主实例</td><td>可读可写的实例</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/236/38331" target="_blank">单节点</a> <li><a href="https://intl.cloud.tencent.com/document/product/236/38329" target="_blank">双节点</a><li><a href="https://intl.cloud.tencent.com/document/product/236/39783" target="_blank">三节点</a></td>
<td>是</td><td>主实例可挂载只读实例，实现读写分离功能</td></tr>
<tr>
<td>只读实例</td><td>仅提供读功能的实例</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38331" target="_blank">单节点</a></td><td>是</td>
<td>只读实例无法单独存在，必须隶属于某个主实例，唯一数据来源是从主实例同步数据，只能与主实例同地域</td></tr>


### 相关信息
- 只读实例的创建操作和注意事项，请参见 [创建只读实例](https://intl.cloud.tencent.com/document/product/236/7270)。
- 只读实例 RO 组的创建和配置，请参见 [管理只读实例](https://intl.cloud.tencent.com/document/product/236/11361)。

  
