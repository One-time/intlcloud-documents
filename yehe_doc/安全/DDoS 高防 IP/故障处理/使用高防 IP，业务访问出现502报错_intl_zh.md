
## 现象描述
使用高防 IP 之后，访问业务出现502报错：Bad Gateway，如图所示：
![](https://main.qcloudimg.com/raw/169adfb6589a9e8220a36b9b034b80dc.png)

## 可能原因
使用高防 IP 后的业务流量走向图：
![](https://main.qcloudimg.com/raw/43a308a282a5d3a9d3d85c735333e91e.png)

### [原因一：回源 IP 被源站拦截或限速](id:yy1)
在配置高防 IP 后，源站服务器的 IP 被高防 IP 在中间代理而被隐藏。所有经过高防 IP 服务访问的客户端源 IP 都会变成高防 IP 的回源 IP。源站服务器接收到的访问请求都是来自高防 IP 回源段，而高防 IP 回源段的 IP 数量有限，分摊过后每个回源 IP 访问源站服务器的请求量较大。

若源站服务器配置了 DDoS 攻击等相关安全防护策略，将有机率触发 DDoS 防护策略，导致将回源 IP 限速甚至拦截。

### [原因二：源站本身异常，导致响应高防的请求超时](id:yy2)
导致异常的可能原因：
1. 在使用高防 IP 之前，源站 IP 暴露，被恶意攻击导致故障。
2. 源站服务器机房物理故障。
3. 服务器内存、CPU 占用过高，导致性能降低。
4. 源站服务器中 Apache、Nginx 等 Web 程序异常。
5. 公网转发至源站服务器间链路出现故障。

### [原因三：网络抖动或者链路故障](id:yy3)
公网网络质量不佳造成的业务访问不稳定，提示502报错。

## 解决思路
### [原因一](#yy1)：解决思路
通过腾讯云拨测平台对源站 IP 和高防 IP 进行拨测，对比源站 IP 和高防 IP 的访问情况。
如源站 IP 正常、高防 IP 大范围异常，则可以判断为高防回源 IP 被源站服务器拦截或限速导致，建议进行高防回源IP加白操作。

详细处理步骤请参见 [原因一：处理步骤](#yy1clbz)。

### [原因二](#yy2)：解决思路
通过将本地主机的解析结果修改为源站来验证源站本身是否正常，首先修改本地 hosts 文件，确认 hosts 绑定已经生效之后，使用域名进行验证源站是否可以正常访问，如不能正常访问，可以尝试做如下处理：
1. 源站 IP 保护。详情步骤请参见 [处理措施1](#clcs1)。
2. 请相关人员进行机房故障检查，修复物理故障。详情步骤请参见 [处理措施2](#clcs2)。
3. 确认 Web 服务是否正常并修复。详情步骤请参见 [处理措施3](#clcs3)。
4. 检查服务器进程占用，内存占用等性能参数是否正常并恢复至正常状态。详情步骤请参见 [处理措施4](#clcs4)。
5. 查看网络层面进行排查或者源站链路监控设备监控到的链路状态，也可通过更换链路测试进行验证与规避。详情步骤请参见 [处理措施5](#clcs5)。

详细处理步骤请参见 [原因二：处理步骤](#yy2clbz)。

### [原因三](#yy3)：解决思路
确定是否存在链路故障情况并联系网络服务商进行修复。

详细处理步骤请参见 [原因三：处理步骤](#yy3clbz)。

## 处理步骤
### [原因一：处理步骤](id:yy1clbz)
将高防 IP 回源段添加至防火墙、主机安全防护软件的白名单中进行放行，下面以 CentOS 6.5 操作系统的防火墙添加白名单为例：
1. 执行如下命令，查看 Linux 防火墙的状态。
```
service iptables status
```
如果控制台提示 Chain INPUT、Chain FORWARD 以及 Chain OUTPUT 项下没有任何规则条目，说明防火墙还未开启。
![](https://main.qcloudimg.com/raw/dbdf7b5f0a4f835c039e10f2de3b4308.png)
2. 执行如下命令，查看防火墙配置文件。
```
cat /etc/sysconfig/iptables
```
根据业务需求，确保防火墙没有额外的黑白名单设置后，将防火墙开启，防止直接打开防火墙之后对业务造成影响。
3. 执行如下命令，开启防火墙。
```
service iptables start
```
![](https://main.qcloudimg.com/raw/7b55af2df725fb8adbdbc82fb34ee000.png)
4. 执行如下命令，再次查看防火墙状态。
```
service iptables status
```
如果控制台提示 Chain INPUT、Chain FORWARD 以及 Chain OUTPUT 任意项显示规则条目，证明防火墙已经打开。
![](https://main.qcloudimg.com/raw/9776ce04d9f8c323f0794e40325aaa9a.png)
5. 执行如下命令，设置 IP 白名单，将回源 IP 段加入防火墙白名单中。
```
Iptables -A INPUT -s 回源IP -j ACCEPT
```
6. 执行如下命令，查看添加的白名单策略，是否成功添加到了防火墙配置中。
```
iptables -nL --line-number
```
如果看到添加的防火墙规则在输出内容内，则代表添加成功。
7. 执行如下命令，保存防火墙配置。
```
service iptables save
```
![](https://main.qcloudimg.com/raw/964ae40a38bad0a39479ec153df16844.png)
8. 执行如下命令，重启防火墙，使配置生效。
```
service iptables restart
```
![](https://main.qcloudimg.com/raw/94cbe1093a28f831ba2b8b9c62388eae.png)

### [原因二：处理步骤](id:yy2clbz)
将本地主机的解析结果修改为源站，来验证源站本身是否正常，首先修改本地 hosts 文件，具体操作如下：
1. 修改本地hosts文件，使本地对业务高防域名的请求到达源站 IP，下面以 Windows 操作系统为例，配置本地 hosts 文件：
打开本地计算机`C:\Windows\System32\drivers\etc`路径下的 hosts 文件，在文末添加如下内容：
![](https://main.qcloudimg.com/raw/8f3d1d4ab7445cf32f1086bdc8cb79f0.png)
例如源站 IP 为10.1.1.1，域名为`www.qqq.com`，则添加：
 ![](https://main.qcloudimg.com/raw/0cef578cfd4d738f448768bad9007cf2.png)
保存 hosts 文件，在本地计算机对被防护的域名运行 ping 命令。
当解析到的 IP 地址是 hosts 文件中绑定的源站 IP 地址时，说明本地 hosts 生效。若没有解析到源站 IP，在 Windows 的命令提示符中运行`ipconfig /flushdns`命令，刷新本地的 DNS 缓存。
2. 确认 hosts 绑定已经生效之后，使用域名进行验证：源站是否可以正常访问，如不能正常访问，针对可能原因对应做如下处理。

#### [处理措施1：源站 IP 保护](id:clcs1)
查看源站流量、请求量是否有大量增长，同时对比高防 IP 管理控制台中的监控。服务器本身流量监控以 CentOS 系统为例，具体操作如下：
1. 常见 Linux 服务器网络流量使用情况可以使用 iftop 进行查看：
```
执行命令：iftop [-i interface]（参数 -i 后跟的 interface 表示网络接口名，如 eth0、eth1 ）
```
输出如下：
![](https://main.qcloudimg.com/raw/b7f421187abc388b9e8faac67f12875c.png)
回显结果说明：
  - 第一行：带宽使用情况显示。
  - 中间部分为外部连接列表，即记录了哪些 IP 正在和本机的网络连接。
  - 中间部分靠右侧部分是实时流量信息，分别是该访问 IP 连接到本机2秒、10秒和40秒的平均流量。
  - => 代表发送数据，<= 代表接收数据 。
  - 底部三行：
    - 第一列：TX 表示发送流量，RX 表示接收流量，TOTAL 表示总流量。
    - 第二列 cumm：表示第一列各种情况的总流量。
    - 第三列 peak：表示第一列各种情况的流量峰值。
    - 第四列 rates：表示第一列各种情况2秒、10秒、40秒内的平均流量。
2. 查看高防 IP 管理控制台的业务流量监控，参考 [查看业务流量情况](https://intl.cloud.tencent.com/document/product/297/37206#viewing-business-traffic-details)。
如果源站遭到大流量攻击，但高防IP管理控制台显示无异常，则有可能是攻击绕过高防IP直接攻击源站。此种源 IP 暴露的处理方法参考 [源站 IP 暴露的解决方法](https://intl.cloud.tencent.com/document/product/297/15568)。

#### [处理措施2：请相关人员进行机房故障检查，修复物理故障](id:clcs2)
对服务器硬件状态进行自查：查看源站服务器机房是否出现断电、网卡、 驱动、内存以及接线等物理硬件故障情况，及时更新或修复。

#### [处理措施3：确认 Web 服务是否正常并修复](id:clcs3)
查看源站服务器的相关监控，CPU/内存的使用率、带宽的使用率等情况。
>?
>- 通常情况下 CPU 或者内存的使用率长时间超过90%，即可判断为状态异常。
>- 带宽使用需要对比业务正常时期业务进程占用情况，查看是否有明显增长，可以参照 [云服务器带宽使用率过高](https://intl.cloud.tencent.com/document/product/248/36207)。

如有异常，进一步处理请您联系相关的技术人员或机房负责人员协助排查问题。

#### [处理措施4：检查服务器进程占用，内存占用等性能参数是否正常并恢复至正常状态](id:clcs4)
对服务器 Web 程序状态进行自查：使用`ps -C nginx -o pid`命令查看服务器 nginx 进程是否正常运行。
如有异常需要联系服务器技术人员，针对源站服务器中 Apache、Nginx 等服务进行修复至业务正常状态水平。

#### [处理措施5：查看网络层面进行排查或者源站链路监控设备监控到的链路状态，也可通过更换链路测试进行验证与规避](id:clcs5)
对公网网络至源站服务器间链路质量，链路连通情况，中间网络设备转发情况等当面进行自查，确保此段链路连通性正常。

### [原因三：处理步骤](id:yy3clbz)
通过腾讯云拨测平台中的站点质量监控对源站 IP 和高防 IP 分别进行公网网络质量的检测和监控。
如果有公网网络质量不佳的情况，进一步需要联系所属运营商进行反馈处理。

