### COSCLI 工具与 COSCMD 工具有什么区别？

1. COSCLI 工具使用 golang 构建，直接发布编译后的二进制包，用户在安装部署时无需预先安装任何依赖，开箱即用；COSCMD 工具使用 Python 构建，用户在安装时需先安装 Python 环境和依赖包。
2. COSCLI 工具支持设置存储桶别名，可以使用一个短字符串来代替`<BucketName-APPID>`，方便用户使用；COSCMD 工具不支持存储桶别名，用户需要输入`<BucketName-APPID>`来指定一个存储桶，命令繁琐且不易阅读。
3. COSCLI 工具支持在配置文件内配置多个存储桶，且支持跨桶操作；COSCMD 工具在配置文件中只能配置一个存储桶，且跨桶操作命令过于冗长。
4. COSCLI 工具将逐步替代 COSCMD 工具，COSCMD 工具将不再新增功能，只修复现有 Bug。


