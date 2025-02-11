安全组是一种虚拟防火墙，具备有状态的数据包过滤功能，用于设置云服务器、负载均衡、云数据库等实例的网络访问控制，控制实例级别的出入流量，是重要的网络安全隔离手段。

您可以通过配置安全组规则，允许或禁止安全组内的实例的出流量和入流量。

## 特点
- 安全组是一个逻辑上的分组，您可以将同一地域内具有相同网络安全隔离需求的云服务器、弹性网卡、云数据库等实例加到同一个安全组内。
- 关联了同一安全组的实例间默认不会互通，您需要添加相应的允许规则。
- 安全组是有状态的，对于您已允许的入站流量，都将自动允许其流出，反之亦然。
- 您可以随时修改安全组的规则，新规则立即生效。

## 使用限制
有关安全组的使用限制及配额，详情请参见 [限制说明](https://intl.cloud.tencent.com/document/product/213/15379)。

## 安全组规则

### 组成部分

安全组规则包括如下组成部分：
- 来源或目标：流量的源（入站规则） 或目标（出站规则），可以是单个 IP 地址、IP 地址段，也可以是安全组，具体请参见 [安全组规则](https://intl.cloud.tencent.com/document/product/215/35513)。
- 协议类型和协议端口：协议类型如 TCP、UDP 等。
- 策略：允许或拒绝。

### 规则优先级

- 安全组内规则具有优先级。规则优先级通过规则在列表中的位置来表示，列表顶端规则优先级最高，最先应用；列表底端规则优先级最低。
- 若有规则冲突，则默认应用位置更前的规则。
- 当有流量入/出绑定某安全组的实例时，将从安全组规则列表顶端的规则开始逐条匹配至最后一条。如果匹配某一条规则成功，允许通过，则不再匹配该规则之后的规则。

### 多个安全组

一个实例可以绑定一个或多个安全组，当实例绑定多个安全组时，多个安全组将按照从上到下依次匹配执行，您可以随时调整安全组的优先级。

## 安全组模板

新建安全组时，您可以选择腾讯云为您提供的两种安全组模版：

- 放通全部端口模版：将会放通所有出入站流量。
- 放通常用端口模板：将会放通 TCP 22端口（Linux SSH 登录），80、443端口（Web 服务），3389端口（Windows 远程登录）、 ICMP 协议（Ping）、放通内网（私有网络网段）。

> ?
> - 如果提供的安全组模版不满足您的实际使用，您也可以新建自定义安全组，详情请参见 [创建安全组](https://intl.cloud.tencent.com/document/product/215/35506)、[安全组应用案例](https://intl.cloud.tencent.com/document/product/215/35519)。
> - 如果您对应用层（HTTP/HTTPS）有安全防护需求，可另行购买 [腾讯云 Web 应用防火墙（WAF）](https://intl.cloud.tencent.com/product/waf)，WAF 将为您提供应用层 Web 安全防护，抵御 Web 漏洞攻击、恶意爬虫和 CC 攻击等行为，保护网站和 Web 应用安全。

## 使用流程
安全组的使用流程如下图所示：
![](https://main.qcloudimg.com/raw/2fccad4c688f66f28cfb3d41dbbb7134.png)

## 安全组实践建议

### 创建安全组
- 调用 API 购买 CVM 时建议指定安全组，未指定安全组时 ，将使用系统自动生成的默认安全组，且默认安全组不可删除。
- 实例防护策略有变更，建议优先修改安全组内规则，不需要重新新建一个安全组。

### 管理规则
- 需要修改规则时可以先将当前安全组导出备份，如果新规则有不利影响，可以导入之前的安全组规则进行恢复。
- 当所需规则条目较多时可以使用 [参数模版](https://intl.cloud.tencent.com/document/product/215/31867)。

### 关联安全组
- 您可以将有相同防护需求的实例加入一个安全组，而无需为每一个实例都配置一个单独的安全组。
- 不建议一个实例绑定过多安全组，不同安全组规则的冲突可能导致网络不通。


