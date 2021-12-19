# SmartIDE Docsy Example

Be a Smart Developer 开发从未如此简单

本代码库为SmartIDE的项目模板库，开发者可以使用 smartide new 命令一键创建项目脚手架，其脚手架代码的内容来自本库。

**说明**: SmartIDE提供跨平台能力，如无特殊说明，以下所列的所有功能默认均可以在Windows和MacOS上执行；对于Linux本地运行模式的支持很快也会发布。

## 基本使用说明

```shell
## 一键启动命令
smartide new hugo -t docsy
```

等待SmartIDE吊起vscode WebIDE后，会在Web Terminal中自动完成以下操作，以下指令在 .ide.yaml 中已经配置好，无需手工运行。

```shell
# 将当前目录初始化成git仓库并使用Git Submodule方式引入Docsy皮肤
# 以下两行命令需要在当前模板初始化完成后从.ide.yaml中删除，因为只有第一次需要执行这2个动作
git init
git submodule add https://gitee.com/smartide/docsy.git themes/docsy

# 初始化git子模块，将子模块中的代码clone到当前仓库中以便程序引用
# 第一次clone子模块需要较长时间，请耐心等待，如果在clone过程中出现失败的情况，请从新运行smartide new指令
git submodule update --init --recursive

# 设置npm使用国内淘宝镜像站，加速npm包获取动作
npm config set registry https://registry.npmmirror.com

# 获取npm包
npm install

# 将当前代码库中的文件及提到到git仓库中
# 以下脚本需要在模块初始化完成后从.ide.yaml中移除
git add . && git commit -m "SmartIDE init"

# 以调试模式启动hugo服务器，默认监听1313端口
 hugo server --bind 0.0.0.0 --disableFastRender --forceSyncStatic --buildDrafts --buildFuture 
```

如果在模块初始化过程中出现问题，最简单的修复方式就是从新运行 smartide new 指令，你可以使用ctrl-c停止当前smartide指令运行，然后运行

```shell
## 删除当前环境，需要在当前目录中运行
smartide remove
## 重置当前smartide环境
smartide reset -ya
```

## 引用说明

本模板源自 [Google Docsy](https://github.com/google/docsy/) 模板，SmartIDE对其进行了本地化处理和扩展。


## 开源协议 & 版权说明

本代码库采用 GPL 3.0 开源协议，具体可以参考 [LICENSE](LICENSE) 文件了解更多细节。

本代码库属于 SmartIDE 产品的一部分，[英捷创软科技(北京)有限公司(简称:LEANSOFT)](https://leansoftx.com)拥有对于 SmartIDE 产品以及其所有相关代码的版权和最终解释权。