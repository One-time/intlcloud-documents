## 查询合作伙伴和子客账单

第一步：存储桶加白。该功能目前在白名单使用阶段，需要开启该功能请联系销售经理加白，加白后的UIN，在账单概览页会出现【账单存储】按钮。

![img](https://docimg9.docs.qq.com/image/FYi6VKGmXyNz1ZKDk6fPbA?w=2712&h=1004)

第二步：角色服务授权。点击【账单存储】按钮后，将会有弹窗提示授权，点击后【前往授权】会在当前页跳转至【角色授权页面】，需要【同意授权】。

第三步：选择存储桶。如没有存储桶，可点击 【Create Bucket】按钮，跳转至创建桶的页面。

第四步：支持存入经销商下客户的账单。勾选【Store Custom Bills】，授权通讯云商务将客户账号的合并账单存入父经销商COS桶。

<img src="https://docimg10.docs.qq.com/image/nQ3lziYhPbxeqOwvVzUclw?w=855&h=964&_type=png" alt="img" style="zoom: 50%;" />

>? 
> - 系统默认将经销商UIN的每日账单、月账单发送到COS桶。另外，腾讯云商务每月确认账单后，会手工触发将客户账号的合并账单存入经销商COS桶。
> - 存储桶同时支持存入子账号的账单。勾选子账号UIN，可将子账号的账单存入父账号COS桶。

### 1、账单存储

​      开通后，每日将更新的数据存入指定的COS桶，共有三种账单，经销模式请关注【合作伙伴经销模式账单】。

​      1）合作伙伴自用日账单：Day+2后，新增的bill_details会存储到COS存储bucket中。比如4月6日，将会有增加一个4月1日 ~ 4月4日的汇总账单；4月8日，将会增加一个4月1日 ~ 4月6日的汇总账单。

​      2）合作伙伴自用月账单：每个月2号更新一份完整的月账单bill_details，如数据量过大，则拆分账单并打包成一个zip文件。

​      3）合作伙伴经销模式账单：每个月月初9号，腾讯云商务确认账单后，会将经销账单存入存储桶中，合作伙伴下载即可：

*文件命名样例：**100010445724-2021-03--by_used_time-bill-details-consolidated_bill-61121cbd9017a16285769571173521960.zip*

![img](https://docimg5.docs.qq.com/image/pc9K4lOvvMZBLjSwjgb78A?w=1704&h=396&_type=png)

### 2、关闭账单存储

​       如用户需要关闭账单功能，点击入口，用户可以点击弹窗中的【关闭存储桶】来关闭该功能。关闭后，该桶保留旧数据，不再写入新数据。

### 3、更换存储桶

​       合作伙伴需要更换桶，点击入口，用户重新选择桶之后，点击【保存设置】即可。历史数据保留在旧桶，新数据将在Day+1 之后写入新桶。

