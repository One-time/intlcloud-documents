>!数据库审计功能重构升级中，敬请期待；在此期间数据库新购实例不再开放审计功能。

<table>
<thead>
<tr>
<th width="22%">实例架构</th>
<th>定义</th>
<th>节点</th>
<th>特点</th>
</tr>
</thead>
<tbody><tr>
<td>标准版（一主一从）</td>
<td>每个分片提供主从双活部署的高可用架构</td>
<td>两个节点：一个 Master 节点，一个 Slave 节点</td>
<td rowspan = "2"><li>支持从机只读</li><li>故障后节点自动恢复</li><li>默认监控采样粒度：5分钟/次</li><li>最大可配备份时长：7天</li><li>操作日志备份：7天</li><li>支持数据库审计，审计日志存储15天，规则配置个数暂无限制</li></td>
</tr>
<tr>
<td>标准版（一主二从）</td>
<td>每个分片提供主从多活部署的高可用架构</td>
<td>三个节点：一个 Master 节点，两个 Slave 节点</td>
</tr>
</tbody></table>

