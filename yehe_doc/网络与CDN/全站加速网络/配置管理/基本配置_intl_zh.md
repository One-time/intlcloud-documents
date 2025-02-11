您可以在 ECDN 控制台中查看域名的基本信息和源站信息，然后根据需要对域名 **所属项目**、**源站类型** 和 **源站地址** 进行修改。
- 基本信息包括：加速域名、CNAME、所属项目及加速服务创建时间。
- 源站信息包括：源站类型和源站地址。

>? 若您的业务已迁移至 CDN 控制台，请参考 [CDN 产品文档](https://intl.cloud.tencent.com/document/product/228)，前往 CDN 控制台进行操作。
## 域名配置页面
1. 登录 [ECDN 控制台](https://console.cloud.tencent.com/dsa)，单击左侧菜单栏的【域名管理】，进入管理页面。
2. 单击您要配置的域名右侧的【管理】，进入域名配置页面。
![](https://main.qcloudimg.com/raw/dd32a2393844fa30784dedd2bdc272cd.png)
3.  域名【基本信息】页面展示域名基本配置信息，包括域名 CNAME、所属项目、加速区域、源站信息、回源 HOST 等。
![](https://main.qcloudimg.com/raw/4a666cb9ee83ebfe8a2bb87b7d3d44d1.png)

## 基本配置项目
### 修改域名所属项目
1. 单击所属项目右侧【修改】。
2. 在弹出的项目列表框中，选择合适的项目名称，单击【确认】提交。 

### 修改域名加速区域
1. 单击加速区域右侧【修改】。
2. 选择域名加速区域，加速区域目前支持中国境内、中国境外和全球选项。
3. 为了避免操作失误，当您需要删除某个加速区域配置时，请提交 [需求工单](https://console.cloud.tencent.com/workorder/category?level1_id=83&level2_id=532&source=0&data_title=%E5%8A%A8%E6%80%81%E5%8A%A0%E9%80%9F%E7%BD%91%E7%BB%9C%20DSA&step=1) 进行修改。

>? 中国境外加速服务限量开放中，若您的账号无法修改加速区域，表示您还未获得中国境外加速权限。您可以通过 [ECDN 全球加速资格申请页面](https://console.cloud.tencent.com/apply) 提交申请，系统将在5个工作日内完成审批，并通过短信和站内信通知您。

### 修改源站配置
1. 单击源站配置右侧修改按钮进入源站修改页面。
2. 在弹框中，修改您的源站类型、回源策略和源站地址信息，如有需要，请查看 [高级回源策略说明](https://intl.cloud.tencent.com/document/product/570/35821)。
3. 修改完成后，单击【确认】提交，系统后台将为域名下发新的源站配置，预计约3 - 5分钟生效。  
![](https://main.qcloudimg.com/raw/d124e64ad4faf93fc7f922a99835099a.png)

### 修改回源配置
单击源站 HOST 后面的【编辑】，在对话框中修改回源 HOST：
![](https://main.qcloudimg.com/raw/30b72a4fa1c6fc59fb2a65160feb736f.png)
![](https://main.qcloudimg.com/raw/eb8bcdb1264cffb77735ae7c376fc02f.png)
