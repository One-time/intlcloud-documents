检索日志时，可能会出现检索不到日志的状态异常。出现该状态异常时，可通过以下几种方式排查问题。

## 确认检索条件

检索不到日志，很多情况下是检索时间范围不正确或检索语句有问题导致。用户先选择较大时间范围（如最近30分钟），检索条件为空，确定是否有日志。



如果检索数据成功，则可能是检索语句或者时间范围有误导致，建议用户查看 [检索语法](https://intl.cloud.tencent.com/document/product/614/30439) 或修改检索时间范围。

## 检查索引配置

索引配置是使用日志服务进行检索分析的必要条件，单击检索页右上方【索引配置】入口，查看索引配置是否开启。索引配置区分全文索引和键值索引，详情可参见 [索引介绍](https://intl.cloud.tencent.com/document/product/614/39594) 文档。



>! 索引配置仅对新写入数据生效，每次更改索引配置，约有1分钟生效延时。
>

## 确认日志采集是否成功

### 云产品日志采集

若您的日志是其他云产品日志，如容器 TKE，负载均衡 CLB 等，可参见 [云产品日志采集指引](https://intl.cloud.tencent.com/document/product/614/38200) 确认是否配置成功，如有问题，请联系 [在线客服](https://intl.cloud.tencent.com/contact-sales)。

### 使用 LogListener 客户端采集日志

 若您是通过 CLS 提供的日志采集客户端 LogListener 采集日志，可按以下步骤排查：
1. 检查机器组状态。
单击检索页右上角【LogListener 采集配置】，确认待采集机器状态是否正常。

>!若待采集日志的机器状态异常，请参见 [机器组异常排查](https://intl.cloud.tencent.com/document/product/614/17424) 文档。	 
2. 检查 LogListener 是否成功拉取采集配置
     在命令行下执行如下命令：
```shell
/etc/init.d/loglistenerd check
```
     如果出现如下图所示“[OK] check loglistener config ok”表示调用拉取配置接口成功。
     ![](https://main.qcloudimg.com/raw/95022fc7832b36e2e8d51b6fe8ed3ab7.jpg)
     返回结果中的 `logconf` 字段为采集配置，如果为空表示没有拉取到对应的采集配置，参考 [LogListener 使用流程](https://intl.cloud.tencent.com/document/product/614/31578) 创建机器组并绑定采集配置。
3. 尽可能确保是最新版本的 LogListener。
     执行以下命令，查看版本号。当前最新版本可查看 [LogListener安装](https://intl.cloud.tencent.com/document/product/614/17414) 文档。
```shell
/etc/init.d/loglistenerd -v
```
>! LogListener 低于2.3.0版本，不能监听软连接方式的日志文件。
>
4. 确认日志上报成功。
 1. 打开 LogListener Debug 日志， 在 LogListener 安装目录下编辑`etc/loglistener.conf`配置文件，将 **level** 设置为 DEBUG，并重启 LogListener。
![](https://main.qcloudimg.com/raw/05bc0bec901147c2b9e6550a85fa7d82.png)
 2. 执行如下命令，重启 LogListener。
```shell
/etc/init.d/loglistenerd restart
```
 3. 执行以下命令，查看日志是否成功上报：
```shell
tail -f log/loglistener.log | grep "ClsFileProc::readFile" | grep send
```
如果日志成功上报到服务后台，则会出现类似下图所示的日志：
![](https://main.qcloudimg.com/raw/109530d249ed468b5ae2c43b3b1e2341.png)
>!如果日志通过 HTTP 方式上报，可以通过抓包查看80端口，判断日志是否上报成功。
>
日志未上报，请按以下步骤排查：

    1. 在安装目录下执行以下命令，检查 LogListener 采集配置是否正确。
```shell
tail -f log/loglistener.log | grep "ClsServerConf::load"
```
如果已配置下发，日志则如下所示：    
![](https://main.qcloudimg.com/raw/d8b24591c6f601af31e57cab8995fd52.png)
下发配置需要检查 log_type、path 信息是否正确：        
       - log_type 表示配置的日志解析类型（单行全文：minimalist_log，分隔符：delimiter_log，json日志：json_log，多行全文：regex_log）。   
       - path 表示日志采集目录。
       
    2. 在安装目录下执行以下命令，检查文件是否被正常监听。
```shell
grep [上报日志文件的文件名] log/loglistener.log
```
如果 grep 失败，使用 `grep regex_match log/loglistener.log` 搜索，检查控制台的正则表达式是否配置合理。如果出现下图所示的内容，表示文件名匹配正则失败，请登录控制台更改表达式。
![](https://main.qcloudimg.com/raw/8b9756fc97dc9fe38e49ddde4fb20335.png)
    3. 检查日志正则解析是否正确。
对于完全正则和多行全文提取模式，需要指定正则表达式。多行全文中，首行正则表达式匹配的是整个首行的内容，而非首行开头的部分内容。
例如，下图所示的日志样例。 INFO、ERROR、WARN 为日志首行，除了匹配（INFO|ERROR|WARN）外，还需将 INFO、ERROR、WARN 后面的字符匹配上。
![](https://main.qcloudimg.com/raw/c43a440e46ca0ff82d21275d90557e44.png)
       -  错误配置方法：`^(INFO|ERROR|WARN)`
       -  正确配置方法：`^(INFO|ERROR|WARN).*`

5. 确认一个文件被一个日志主题采集、单行日志最大不超过1M。
   未按上述要求可能导致采集缺失。



