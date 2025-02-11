本文介绍云服务器的出网和入网带宽上限、不同计费模式下的带宽峰值区别。

## 出网带宽上限（下行带宽）

您设置的公网网络带宽上限默认为出网带宽上限，即从云服务器流出的带宽。公网网络的带宽上限根据不同的网络计费模式有所不同。具体信息如下：
- 2020年2月24日00:00以后创建的机器按以下规则执行：
<table>
<tbody><tr><th rowspan="2" style="
    width: 20%;
">网络计费模式</th><th colspan="2">实例</th><th rowspan="2" style="width:35%">带宽上限的可设置范围（Mbps）</th></tr>
<tr><th style="
    width: 20%;
">实例计费模式</th><th style="
    width: 25%;
">实例配置</th></tr>
<tr><td>按流量计费</td><td>按量计费实例</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>按带宽计费</td><td>按量计费实例</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>共享带宽包</td><td colspan="2">ALL</td><td>0 - 2000</td></tr>
</tbody></table>

- 2020年2月24日00:00以前创建的机器按以下规则执行：
<table>
<tbody><tr><th rowspan="2" style="
    width: 20%;
">网络计费模式</th><th colspan="2">实例</th><th rowspan="2" style="width:35%">带宽上限的可设置范围（Mbps）</th></tr>
<tr><th style="
    width: 20;
">实例计费模式</th><th style="
    width: 25%;
">实例配置</th></tr>
<tr><td rowspan="1">按流量计费</td><td>按量计费实例</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td rowspan="3">按带宽计费</td><td>按量计费实例</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>共享带宽包</td><td>ALL</td><td>0 - 1000</td></tr>
</tbody></table>



## 入网带宽上限（上行带宽）

公网的入网带宽是指流入云服务器实例的带宽。
- 用户购买的带宽大于10Mbps时，腾讯云会分配与购买的带宽相等的外网入方向带宽。
- 用户购买的带宽小于等于10Mbps时，腾讯云会分配10Mbps外网入方向带宽。

## 带宽峰值
带宽峰值主要分为按流量计费和按带宽计费两种类型。不同类型的带宽峰值含义有所不同，具体区别如下：

<table>
       <tbody><tr>
			 <th width="17%">计费模式</th>
			 <th>带宽峰值区别</th>
			 <th>说明</th>
       </tr>
			 <tr>
			 <td>按流量计费</td>
			 <td>带宽峰值仅作为带宽<strong>最高上限</strong>峰值，不作为承诺指标。当出现带宽资源争抢时，带宽峰值可能会受到限制。</td> 
			 <td>单个地域中，所有按流量计费的云服务器、弹性公网 IP、弹性公网 IPv6 实例，实际运行的总带宽峰值不大于5Gbps。若您的业务要求带宽保障或需更大带宽峰值，请购买按固定带宽计费的公网带宽。</td> 
			 </tr>
       <tr>          
            <td>按带宽计费<br/>（包括包月带宽和按小时带宽）</td>
            <td>带宽峰值作为承诺指标。当出现带宽资源争抢时，带宽峰值有保证，不会受到限制。</td>
						<td>单个地域中，所有按固定带宽计费（包括包月带宽和按小时带宽）的云服务器、弹性公网 IP 实例，购买和实际运行的总带宽峰值不大于50Gbps。若您有更大带宽需求，请联系您的商务经理申请调整。

</td> 
            </tr> 
</tbody></table>


## 相关文档
[调整公网带宽](https://intl.cloud.tencent.com/document/product/213/15517)
