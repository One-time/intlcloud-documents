专线网关用于连接腾讯云 VPC 与物理专线（专用通道），是专线网络的流量入口。专线网关分为私有网络专线网关和云联网专线网关，您可以根据不同的场景进行选择。

## 使用限制
标准型专线网关支持传递辅助 CIDR，但需要遵循如下限制：
- 金融云地域的标准型专线网关不支持传递辅助 CIDR。
- 标准型专线网关支持传递10个辅助 CIDR。
- NAT 型专线网关不支持传递辅助 CIDR。


## 私有网络专线网关
在专线网络架构中，专用通道的模式对 IDC 到腾讯云 VPC 方向的路由目的网段有影响，具体如下表所示：
<table>
<tr>
<th>专用通道模式</th>
<th>IDC 侧上云路由</th>
</tr>
<tr>
<td>静态</td>
<td>IDC 到腾讯云 VPC 方向的路由规则，由用户在本地路由器配置。</td>
</tr>
<tr>
<td>BGP</td>
<td>IDC 侧通过 BGP 协议学习到 VPC CIDR。</td>
</tr>
</table>
例如某专线网络架构中，使用私有网络专线网关实现腾讯云 VPC 与一个数据中心连接，不同模式的专用通道下路由配置如下：

- 若专用通道为静态模式，IDC 到腾讯云 VPC 方向的路由目的网段，由用户在本地路由器配置，如 VPC CIDR（172.21.0.0/16）。
<img width="80%" src="https://main.qcloudimg.com/raw/71f3699ac26a9df2fbb410ba3b31bf27.png" style="zoom:67%;" />
- 若专用通道为 BGP 模式，IDC 到腾讯云 VPC 方向的路由目的网段，为本地路由器通过 BGP 协议学习到的 VPC CIDR（172.21.0.0/16）。
<img width="80%" src="https://main.qcloudimg.com/raw/ab36e0aa7080f7804a2073692455f62a.png" style="zoom:67%;" />

## 云联网专线网关
一个云联网专线网关可以关联一个云联网和多个专用通道，实现云联网内的多个 VPC 与不同的 IDC 互联。在专线网络架构中，创建云联网专线网关的时间、专用通道的模式均对 IDC 到腾讯云 VPC 方向的路由目的网段有影响，具体如下表所示：
<table>
<tr>
<th>创建时间</th>
<th>专用通道模式</th>
<th>IDC 侧上云路由</th>
</tr>
<tr>
<td rowspan="2">2020 年 9 月 15 日零点前</td>
<td>静态</td>
<td>IDC 到腾讯云 VPC 方向的路由规则，由用户在本地路由器配置。</td>
</tr>
<tr>
<td>BGP</td>
<td>IDC 侧通过 BGP 协议学习到 VPC 子网 CIDR。</td>
</tr>
<tr>
<td rowspan="2">2020 年 9 月 15 日零点后</td>
<td>静态</td>
<td>IDC 到腾讯云 VPC 方向的路由规则，由用户在本地路由器配置。</td>
</tr>
<tr>
<td>BGP</td>
<td>	IDC 侧通过 BGP 协议学习到 VPC CIDR。</td>
</tr>
</table>
例如在某专线网络架构中，专线网关 A 为 2020 年 9 月 15 日零点前创建，专线网关 B 为 2020 年 9 月 15 日零点后创建。不同专用通道模式的路由流转如下：

- 当专用通道 A 和专用通道 B 均为静态模式时，IDC 到腾讯云 VPC 方向的路由目的网段为用户在本地路由器配置的 VPC CIDR（172.21.0.0/16）。专线网关 A 和专线网关 B 的路由完全一致，因此本地 IDC 的流量均匀发送至两个专线网关。
<img width="80%" src="https://main.qcloudimg.com/raw/b1802fe849f2ef09589fa9b9061c827d.png" style="zoom:67%;" />
- 当专用通道 A 和专用通道 B 均为 BGP 模式时，本地路由器通过 BGP 协议从专线网关 A 学习到的路由目的网段为子网 CIDR（172.21.0.0/20、172.21.16.0/20），从专线网关 B 通过 BGP 路由协议学习到目的网段为 VPC CIDR（172.21.0.0/16）。由于本地路由器按最长掩码匹配原则进行转发，因此流量将全部转发至专线网关 A。当专用通道 A 故障时，IDC 侧去往专线网关A 的路由条目消失，上云流量才会转发至专线网关 B。
>?如果您的专线网关在 2020年9月15日零点前所创建，请提交 [工单申请 ](https://console.cloud.tencent.com/workorder/category)将专线网关对外发布路由规则更改为 VPC CIDR。
>
<img width="80%" src="https://main.qcloudimg.com/raw/cf9aff5217e067582a04f8c50551f56b.png" style="zoom:67%;" />
