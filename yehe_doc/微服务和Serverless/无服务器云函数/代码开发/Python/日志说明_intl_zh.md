## 日志开发

您可以在程序中使用以下语句来完成日志输出：
- print
- logging 模块

例如，执行以下代码，您可在函数日志中查询输出内容。
<dx-codeblock>
::: python
import logging
logger = logging.getLogger()
logger.setLevel(logging.INFO)

def main_handler(event, context):
	logger.info('got event{}'.format(event))
	print("got event{}".format(event))
	return 'Hello World!'  
:::
</dx-codeblock>



## 日志查询

当前函数日志均会投递至腾讯云日志服务 CLS 中，您可对函数日志进行投递配置，详情可参见 [日志投递配置](https://intl.cloud.tencent.com/document/product/583/39778)。
您可通过云函数的日志查询界面或通过日志服务的查询界面，查询函数执行日志。日志查询方法详情可参见 [日志检索教程](https://intl.cloud.tencent.com/document/product/583/39777)。

>? 函数日志投递到日志服务日志集 LogSet 和日志主题 LogTopic，均可以通过函数配置查询。


## 自定义日志字段

当前在函数代码中通过简单的 `print`，或通过 `logger` 输出的字符串内容，将会在投递到日志服务时，记录在 `SCF_Message` 字段中。日志服务的字段说明可见 [索引说明](https://intl.cloud.tencent.com/document/product/583/39778#.E7.B4.A2.E5.BC.95.E9.85.8D.E7.BD.AE)。

目前云函数已经支持在输出到日志服务的内容中增加自定义字段，通过增加自定义字段，您可以将业务字段及相关数据内容输出到日志中，并通过使用日志服务的检索能力，对执行过程中的业务数据及相关内容进行查询跟踪。

### 输出方法

当函数输出的单行日志为 JSON 格式时，JSON 内容将被解析并在投递至日志服务时按`字段:值`的方式进行投递。JSON 内容的解析仅能解析第一层，更多的嵌套结构将作为值进行记录。

您可执行以下代码进行测试：
<dx-codeblock>
::: python
# -*- coding: utf8 -*-
import json
		
def main_handler(event, context):
	print(json.dumps({"key1": "test value 1","key2": "test value 2"}))
	return("Hello World!")
:::
</dx-codeblock>

### 检索方法

在使用上述代码进行测试运行时：
- 您可在日志服务中检索 `key1` 和 `key2` 两个字段。
- 您也可以在日志服务中启用键值索引，并使用 `key1`、`key2` 作为关键字进行检索，详情可参见 [日志服务索引配置](https://intl.cloud.tencent.com/document/product/614/39594)。
>! 修改索引配置后，仅对新写入的数据生效。



**检索结果**
在测试写入日志服务后，您可以在日志查询中检索到 `key1`、`key2` 字段。如下图所示：
![](https://main.qcloudimg.com/raw/3cfe31543cb065044fab27b52a7a4242.png)

