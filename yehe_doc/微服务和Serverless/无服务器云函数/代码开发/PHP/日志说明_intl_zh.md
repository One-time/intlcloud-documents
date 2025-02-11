## 日志开发

您可以在程序中使用以下语句来完成日志输出：

- echo 或 echo()
- print 或 print()
- print_r()
- var_dump()

例如，执行以下代码，可以在函数日志中查询输出内容。

```php
<?php
function main_handler($event, $context) {
    print_r ($event);
    print_r ($context);
    echo "hello world\n";
    print "hello world\n";
    var_dump ($event);
    return "hello world";
}
?> 
```



## 日志查询

当前函数日志均会投递至腾讯云日志服务 CLS 中，您可对函数日志进行投递配置，详情可参见 [日志投递配置](https://intl.cloud.tencent.com/document/product/583/39778)。
您可通过云函数的日志查询界面或通过日志服务的查询界面，查询函数执行日志。日志查询方法详情可参见 [日志检索教程](https://intl.cloud.tencent.com/document/product/583/39777)。

>? 函数日志投递到日志服务日志集 LogSet 和日志主题 LogTopic，均可以通过函数配置查询。

## 自定义日志字段

当前在函数代码中通过简单的 echo，print 等输出的内容，将会在投递到日志服务时，记录在 `SCF_Message` 字段中。日志服务的字段说明可见 [索引说明](https://intl.cloud.tencent.com/document/product/583/39778)。

目前云函数已经支持在输出到日志服务的内容中增加自定义字段，通过增加自定义字段，您可以将业务字段及相关数据内容输出到日志中，并通过使用日志服务的检索能力，对执行过程中的业务数据及相关内容进行查询跟踪。

### 输出方法

当函数输出的单行日志为 JSON 格式时，JSON 内容将被解析并在投递至日志服务时按“**字段:值**”的方式进行投递。JSON 内容的解析仅能解析第一层，更多的嵌套结构将作为值进行记录。

您可执行以下代码进行测试：

```php
<?php
function main_handler($event, $context) {
    $custom_key = array('key1' => 'test value 1', 'key2' => 'test value 2');
    echo json_encode($custom_key);
    return "hello world";
}
?>
```

### 检索方法

在使用上述代码进行测试运行时：

- 可以在日志服务的字段日志中检索 `key1` 和 `key2` 两个字段。
- 也可以在日志服务中启用键值索引，并使用 `key1`、`key2` 作为关键字进行检索，详情可参见 [日志服务索引配置](https://intl.cloud.tencent.com/document/product/614/39594)。

>! 修改索引配置后，仅对新写入的数据生效。

**检索结果**
在测试写入日志服务后，您可以在日志查询中检索到 `key1`、`key2` 字段。如下图所示：
![](https://main.qcloudimg.com/raw/6667c6e20650eedb43f5e4f3bb4fa047.png)
