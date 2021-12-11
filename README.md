![](smartide-logo-small.png)
<p align="center">
  中文 ｜ <a href="README-EN.md">English</a>
</p>
<h3 align="center">Be a Smart Developer, 开发从未如此简单</h3>
<p align="center">
  中国主页: <a href="https://smartide.cn/zh/" target="_blank">https://smartide.cn</a> 
  海外主页: <a href="https://smartide.dev/en/" target="_blank">https://smartide.dev</a> 
</p>
<p align="center">  
  <a href="https://gitee.com/smartide" target="_blank"><img src="https://img.shields.io/badge/git-Gitee-red?logo=gitee" /></a> 
  <a href="https://github.com/smartide" target="_blank"><img src="https://img.shields.io/badge/git-GitHub-blue?logo=github" /></a> 
</p>
<p align="center">
  <img src="https://dev.azure.com/leansoftx/smartide/_apis/build/status/smartide-codesign-ci?branchName=main" />
  <img src="https://github.com/smartide/smartide-templates/actions/workflows/sync2gitee.yml/badge.svg" />
  <br/>
  <img src="https://dev.azure.com/leansoftx/945b0f40-4baa-4f8a-be2c-4997b4c0af6a/23e62cbd-3bd8-42a3-a414-df7a1957a69b/_apis/work/boardbadge/37313877-3fed-46f3-87c0-dd28ce47e264" />
</p>
<hr />

# SmartIDE 项目模板库

本代码库为SmartIDE的项目模板库，开发者可以使用 smartide new 命令一键创建项目脚手架，其脚手架代码的内容来自本库。

**说明**: SmartIDE提供跨平台能力，如无特殊说明，以下所列的所有功能默认均可以在Windows和MacOS上执行；对于Linux本地运行模式的支持很快也会发布。

## 工作机制

当开发者使用 smartide new 命令时，SmartIDE会自动将本Git库的内容克隆到当前用户的~/.ide/目录下面，并读取其中的 template.json 文件获取所有可用的模板列表。

开发者可以打开本地计算机上的 终端应用（Windows使用PowerShell，MacOS使用Terminal) 使用以下命令获取这个列表

```shell
smartide new

SmartIDE工作区模板

SdkName      TypeName
node         _default
node         express
node         base
java         _default
golang       _default
php          _default

选项：
  -d, --debug         是否开启Debug模式，在该模式下将显示更多的日志信息
  -h, --help          打印当前说明文字
  -t, --type string   类型
```

开发者可以从以上列表中选择所需要的模板，通过以下命令一键创建开发环境

```shell
## 创建空目录并进入此目录
## 提示: 如果执行smartide new的目录不是空目录，smartide会给出警告提示，但是仍然允许用户继续进行操作。
mkdir new-app
cd new-app

## 使用特性sdk的空模板创建工作区
smartide new <sdkName>

## 使用特定sdk的特定模板创建工作区
smartide new <sdkName> -t <TypeName>
```

## 示例

请参考 [Node.Js快速启动手册](https://smartide.cn/zh/docs/quickstart/new-node/) 了解如何使用 smartide new 命令快速创建一个基于 node express 框架的应用程序开发工作区。

## 如何添加你自己的模板

SmartIDE模板库为开源免费代码，欢迎任何人通过提交 Issue 或者发送 Pull Request 的方式扩充这个模板库。

### 模板库目录结构

- 模板库采用2级目录结构
  - 第一级代表sdk类型，比如: golang, java, node, php, python
  - 第二级为具体template的文件夹，第二级目录的名称可以随意指定，不能有空格和特殊字符，只能使用字符名称，暂时不支持中文目录名称
- template文件夹结构
  - 一个template文件夹其实就是一个可工作的代码库
  - 为了能够适配 SmartIDE，这里需要添加一个 .ide 目录并在其中创建1个文件
    - .ide.yaml - 此文件为SmartIDE的配置文件，其内容描述了SmartIDE如何启动当前项目的开发环境

以下是一个典型的 node.js 的 .ide.yaml 文件的示例，其他sdk类型的配置文件请见具体sdk目录下的_default目录。

```yaml
version: smartide/v0.3
orchestrator:
  type: docker-compose
  version: 3
workspace:
  dev-container:
    service-name: smartide-template-node
    ports:
      webide: 6800
      ssh: 6822
    ide-type: vscode
    volumes: 
      git-config: true
      ssh-key: true
      
  services:
    smartide-template-node:
      image: registry.cn-hangzhou.aliyuncs.com/smartide/smartide-node:latest
      restart: always
      environment:
        ROOT_PASSWORD: root123
      volumes:
        - .:/home/project
      expose:
        - 3000
      ports:
        - 3001:3001
      networks:
        - smartide-network  
  networks:
    smartide-network:
      external: true
```

### 制作并测试自己的模板

1. 按照 [安装手册](https://smartide.cn/zh/docs/install/) 安装 SmartIDE 命令行工具 
2. 执行 smartide new 让 SmartIDE 完成当前模板的下载
3. 进入 ~/.ide/template 目录，执行 git checkout -b {分支名称} 创建一个新分支

```shell
git checkout -b {分支名称}
```
4. 在所创建的分支中按照以上模板结构创建自己的模板文件夹
5. 更新 template.json 以便 SmartIDE 命令行工具可以识别你的模板
6. 使用 smartide new {SdkName} -t {TypeName} 测试模板是否可以正常工作

```shell
smartide new {SdkName} -t {TypeName}
```

### 提交PR

**提示**: 为了方便中国大陆地区的开发者提交贡献，我们提供了Gitee的代码库地址，此代码库与GitHub上的代码库自动保持同步。但是为了避免双向同步造成的代码冲突，所有提交到Gitee的PR内容会优先合并到GitHub主库，再同步回到Gitee。

1. 通过SmartIDE在 Github 或者 Gitee 的代码库创建你的fork
2. 在你本地的 ~/.ide/template 目录中运行以下命令添加指向自己的fork库的GitURL

```shell
git remote add my-smartide <你的Fork库的GitURL>
```

3. 推送你本地用于测试的分支到你的fork库，并通过你的fork库提交PR给SmartIDE主库

```shell
git push -u my-smartide {分支名称}
```

开发者完成以上操作以后，SmartIDE产品团队会审核并测试你的代码，如果符合我们的质量标准，我们会接受PR并合并进入SmartIDE的模板库，这样全球的开发者就都可以使用你的新模板了。

## 开源协议 & 版权说明

本代码库采用 GPL 3.0 开源协议，具体可以参考 [LICENSE](LICENSE) 文件了解更多细节。

本代码库属于 SmartIDE 产品的一部分，[英捷创软科技(北京)有限公司(简称:LEANSOFT)](https://leansoftx.com)拥有对于 SmartIDE 产品以及其所有相关代码的版权和最终解释权。





