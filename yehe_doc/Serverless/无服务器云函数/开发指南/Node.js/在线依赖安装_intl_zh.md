## 操作场景

腾讯云云函数提供函数部署时在线安装依赖的功能。

## 功能特性

>?目前仅针对 Node.js 具备在线安装依赖功能。

如果在函数配置中启用了“在线安装依赖”，在每次上传代码后，云函数后台将检查代码包根目录的 `package.json` 文件，并根据 `package.json` 中的依赖，尝试使用 npm install 安装依赖包。

例如，项目中的 `package.json` 文件中列出了如下依赖包：

```
{
      "dependencies": {
      "lodash": "4.17.15"
    }
}
```



此依赖包会在部署时导入函数中：

```
const _ = require('lodash');
exports.handle = (event, context, callback) => {
    _.chunk(['a', 'b', 'c', 'd'], 2);
    // => [['a', 'b'], ['c', 'd']]
};
```

## 操作步骤

您可通过以下两种方式实现云函数安装依赖包功能。
<dx-tabs>
:::开启自动安装依赖
1. 登录 [云函数控制台](https://console.cloud.tencent.com/scf/index)，选择**广州**地域。
2. 选择左侧导航栏【函数服务】，在“函数服务”列表页面选择函数名。
3. 选择【函数代码】页签，根据您的实际需求修改函数代码。
4. 在 IDE 代码编辑窗口右上角中单击【<img src="https://main.qcloudimg.com/raw/2b9a01a346ba19c9050c6c160ec54f48.jpg" width="2%"></img>】，在下拉列表中选择【自动安装依赖:关闭】以开启自动安装依赖，如下图所示：
![](https://main.qcloudimg.com/raw/a6e558badfef96cbbcc85bbe31a11b16.png)
5. 单击【部署】，云函数后台会根据 `package.json` 自动安装依赖。
:::
:::使用\snpm\s直接安装\sNode.js\s依赖包
1. 在 IDE 代码编辑窗口顶部菜单栏中选择【终端】页签，在下拉列表中选择【新终端】。
2. 在打开的终端中执行以下命令，进入函数根目录 `/src`。
``` plaintext
  cd src
```
3. 执行 `npm` 命令安装 Node.js 依赖包，例如，执行以下命令将添加 lodash 依赖包：
``` plaintext
  npm install lodash
```
![](https://main.qcloudimg.com/raw/530d6878c6d9711045a4cac6c9000071.png)
4. 单击【部署】即可将安装成功的依赖包和函数一起打包同步至云端。
:::
</dx-tabs>
