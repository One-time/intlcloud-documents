
### 插件支持在同一个 Panel 中多地域查询吗？

如果在 Dashboard 中使用 `region` 模板变量，则仅支持单地域查询。多地域实例对比可在同一个 Panel 中建多个 Query Target。

### 插件支持在同地域多个实例对比吗？

可以将模板变量中 `Selection Options` 下的 `Multi-value` 设置为 true。
![](https://qcloudimg.tencent-cloud.cn/raw/40c4ef15f5d86c7c6e6f616a78c697f3.png)
 Dashboard 中下拉框便可以进行多选实例，如图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/52f6b4b6427f4167375aa161d3be2219.png)

### 对比多个实例时，为什么 Panel 中报错 `Only queries that return single series/table is supported` ？
![](https://main.qcloudimg.com/raw/35b75a1b7840e96df8b64940664233c7.png)

部分 Panel 类型如`仪表盘`图表仅支持单 query 查询，如需对比多实例请使用折线图 (Line)。

###  模板变量中的实例下拉框的选项显示的是 `InstanceId` ，如何展示 `InstanceName` ？

 可以在模板变量中使用 `InstanceAlias=InstanceName` ，或者使用 `display` 属性进行拼接，例：
  1. `Namespace=QCE/CVM&Action=DescribeInstances&Region=$region&InstanceAlias=InstanceName`
  2. `Namespace=QCE/CVM&Action=DescribeInstances&Region=$region&display=${InstanceId}-${InstanceName}`

>?如果同时存在 `InstanceAlias` 和 `display` 字段，则仅会展示 `display` 的值。
