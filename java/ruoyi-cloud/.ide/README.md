# SmartIDE 快速启动RuoYi-cloud项目
## 若依微服务项目介绍:
- 若依微服务版本：使用的前端技术Vue、Element、后端Spring Cloud & Alibaba微服务的权限管理系统。详细介绍见:http://doc.ruoyi.vip/ruoyi-cloud/ 。
- 项目本身包括多个微服务
```
com.ruoyi     
├── ruoyi-ui              // 前端框架 [80]
├── ruoyi-gateway         // 网关模块 [8080]
├── ruoyi-auth            // 认证中心 [9200]
├── ruoyi-api             // 接口模块
│       └── ruoyi-api-system                          // 系统接口
├── ruoyi-common          // 通用模块
│       └── ruoyi-common-core                         // 核心模块
│       └── ruoyi-common-datascope                    // 权限范围
│       └── ruoyi-common-log                          // 日志记录
│       └── ruoyi-common-redis                        // 缓存服务
│       └── ruoyi-common-security                     // 安全模块
│       └── ruoyi-common-swagger                      // 系统接口
├── ruoyi-modules         // 业务模块
│       └── ruoyi-system                              // 系统模块 [9201]
│       └── ruoyi-gen                                 // 代码生成 [9202]
│       └── ruoyi-job                                 // 定时任务 [9203]
├── ruoyi-visual          // 图形化管理模块
│       └── ruoyi-visual-monitor                      // 监控中心 [9100]
├──pom.xml                // 公共依赖
```
- 同时包含多个组件包括Mysql、Redis、Nacos、Node、Maven以及Sentinel。

> 启动这样一个项目，不免要进行繁杂的组件安装与配置。
> **注意**，该项目启动最低要求2CPU,8G内存。
## SmartIDE快速启动RuoYi-Cloud项目
下面我们使用SmartIDE快速启动这个项目，只需要一个命令行，或者在Server上通过点击，即可实现以上全部操作。

这里我们为项目配备了MySQL客户端工具，同时也包含了Sonar静态代码扫描工具。

为了满足Sonar静态扫描工具的要求，需要在资源中，进行以下配置：
```shell
vim /etc/sysctl.conf
```
添加以下内容即可：
```shell
# 限制一个进程可以拥有的VMA(虚拟内存区域)的数量
vm.max_map_count=262144
# 设置系统所有进程一共可以打开的文件数量
fs.file-max = 6553600
```

启动方式：
- 1.命令行
```shell
mkdir ruoyi-cloud
smartide new java -t ruoyi-cloud
```
- 2.Server

  [模板库]-[基于微服务架构的java环境]-[初始化工作区] 选择工作区使用资源，创建即可。
