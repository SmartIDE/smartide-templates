![](smartide-logo-small.png)
<p align="center">
  <a href="README.md">中文</a> ｜ English
</p>
<h3 align="center">Be a Smart Developer, 开发从未如此简单</h3>
<p align="center">
  China: <a href="https://smartide.cn/zh/" target="_blank">https://smartide.cn</a> 
  Global: <a href="https://smartide.dev/en/" target="_blank">https://smartide.dev</a> 
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

# SmartIDE Templates

This repository contains templates for SmartIDE, you can use [smartide new] command to create new workspaces based on these templates.

**Note**: SmartIDE is a cross-platform tool, all comamnds listed in this document works on Windows & MacOS, Linux support is coming soon.

## How the template works?

When you run [smartide new] command, SmartIDE will clone this repo into *~/.ide/* of current user, and read the template list from *template.json*.

Then you can run the following command to list all available templates.

```shell
smartide new

SmartIDE Workspace Templates

SdkName      TypeName
node         _default
node         express
node         base
java         _default
golang       _default
php          _default

Options:
  -d, --debug         Enable debug mode, show more log messages
  -h, --help          Print the current help message
  -t, --type string   Specify template TypeName
```

You can choose from the options above to create new SmartIDE workspace.

```shell
## Create a empty folder
## Note: if SmartIDE detects the current folder is not empty, it will warn you butyou can still continue.
mkdir new-app
cd new-app

## Create an empty SmartIDE Workspace with the specified SDK
smartide new <sdkName>

## Create a project from the specified tempalte type
smartide new <sdkName> -t <TypeName>
```

## Quick Start Sample

Please refer to [Node.Js快速启动手册](https://smartide.cn/zh/docs/quickstart/new-node/) for more details about how to create a new SmartIDE workspace based on 'node express' framework.

## Contribution Guide

SmartIDE template is open-source and free, you can create Issue or send Pull Request to this repo to add your templates.

### Template Structure

- 2 level folder structure
  - 1st level (sdk level) specify sdk type, e.g. golang, java, node, php, python etc.
  - 2nd level (template level) specify the actual template file system under a named folder. You can name your template with anything you want, but please do not include space or special charactors in the folder name.
- template level folder structure
  - Each folder contains a set of file system which should be a working project for a specific sdk, the folder must includes the following file
    - a *.ide.yaml* file under */.ide/* folder, which is the configuration file for SmartIDE.
    - SmartIDE will use this file to generate your workspace.

Here is an sample *.ide.yaml* file for node.js SDK, you can refer the *_default* folder under each of the SDK folder to get more samples.

```yaml
version: smartide/v0.3
orchestrator:
  type: docker-compose
  version: 3
workspace:
  dev-container:
    service-name: smartide-template-node
    ports:
      tools-webide-port: 6800
      tools-ssh: 6822
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
        - 6822:22
        - 6800:3000
        - 3001:3001
      networks:
        - smartide-network  
  networks:
    smartide-network:
      external: true
```

### Develop and Test your template

1. Follow [安装手册](https://smartide.cn/zh/docs/install/) to install SmartIDE cli tool.
2. Run *smartide new* to allow SmartIDE clone this template repo to your *~/.ide/* folder
3. cd into *~/.ide/template* and create a new git branch

```shell
git checkout -b {branchName}
```
4. Create your own template folder in this newly created branch.
5. Add your template mainifest into *template.json* to allow SmartIDE use your template.
6. Run *smartide new {SdkName} -t {TypeName}* to test your template is working correctly.

```shell
smartide new {SdkName} -t {TypeName}
```

### Submit your template via Pull Request

1. Fork this repo
2. Add your fork's GitURL to a remote in *~/.ide/template*

```shell
git remote add my-smartide <GitURL of your fork>
```

3. Push your branch to your fork and create a PR to this repo.

```shell
git push -u my-smartide {branchName}
```

Once you submit your template as a Pull Requst, SmartIDE team member will review and test your template to make sure it's working properly and accpet your PR. Then your template will be available to all other developers.


## License

Copyright &copy; [leansoftX.com](https://leansoftX.com). All rights reserved.

Licensed under the [GPL 3.0](LICENSE) license.