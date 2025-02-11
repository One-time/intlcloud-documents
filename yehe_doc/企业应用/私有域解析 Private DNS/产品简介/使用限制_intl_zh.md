### 私有域解析 Private DNS 限制
当前使用私有域解析 Private DNS 存在如下限制：
>!
>- 腾讯云默认 DNS 为：`183.60.83.19`，`183.60.82.98`，若不使用腾讯云默认 DNS，将无法使用私有域解析 Private DNS 提供的服务。如需修改，请您参考 [获取内网 IP 地址和设置 DNS](https://intl.cloud.tencent.com/document/product/213/17941)。
>- 如您有更进一步的业务场景需求，可通过商务渠道或 [提交工单](https://console.cloud.tencent.com/workorder/category) 进行反馈。

<table>
<thead>
  <tr>
    <th width="17%">限制项</th>
    <th>限制阈值</th>
		<th>说明</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>解析记录数量</td>
    <td>10万条</td>
    <td>同一个 UIN 账号下最多支持添加10万条 DNS 解析记录。</td>
  </tr>
  <tr>
    <td>域名数</td>
    <td>500个</td>
    <td>同一个 UIN 账号下最多仅支持创建私有域名数量为500个。</td>
  </tr>
  <tr>
    <td>TTL</td>
    <td>1 - 86400s</td>
    <td>解析记录在 DNS 服务器中的存留时间，支持自定义输入。</td>
  </tr>
	  <tr>
    <td>开放地域</td>
    <td>雅加达、东京、中国香港、新加坡</td>
		<td>开放地域即为私有域可关联 VPC 地域。</td>
  </tr>
		  <tr>
    <td>创建私有域</td>
    <td>仅支持创建符合 IANA 标准规范的域名（.com.cn 此类除外）</td>
		<td>参考资料：<a href="https://www.iana.org/domains/root/db">根域名数据库</a>。</td>
  </tr>
</tbody>
</table>

### 负载均衡限制
>?“负载均衡” 条数：相同主机、相同记录类型允许添加的条数。

<table>
<thead>
  <tr>
    <th width="17%">记录类型</th>
    <th>“负载均衡” 条数</th>
		<th>备注</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>A</td>
    <td>10</td>
		<td>-</td>
  </tr>
  <tr>
    <td>AAAA</td>
    <td>10</td>
		<td>-</td>
  </tr>
  <tr>
    <td>TXT</td>
    <td>20</td>
		<td>TXT 负载均衡不支持权重设置。</td>
  </tr>
	  <tr>
    <td>CNAME</td>
    <td>5</td>
		<td>-</td>
  </tr>
		  <tr>
    <td>MX</td>
    <td>50</td>
		<td>-</td>
  </tr>
		  <tr>
    <td>PTR</td>
    <td>PTR 记录不支持负载均衡。</td>
		<td>-</td>
  </tr>
</tbody>
</table>
