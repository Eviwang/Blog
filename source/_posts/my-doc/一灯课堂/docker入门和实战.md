前言 ：

严格来说：技术本身不值钱，因为干的活值钱，商业模式值钱。才会导致程序员 工资高

中小型公司的通病：对于技术总是去尝试，去用，去乱用，不管适不适合。

预则立不预则废

凡是都要有计划，然后再开始实施，会事半功倍 。



## 微服务核心思想

- 微服务属于架构层面的设计模式
- 微服务 的设计概念以业务功能为主
- 微服务独立提供对应的业务功能
- 微服务不拘泥于具体的语言实现
- 微服务架构 约等于 【 模块化开发(业务模块) + 分布式计算 】



![1577589969952](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\1577589969952.png)

### 微服务的特点 

- 小，专注于一件事 （甚至可以小到只有一个接口）
- 处于独立的进程中
- 轻量级的通信机制
- 松耦合，独立部署



### 合理使用 微服务

- 业务复杂度高
- 团队规模大
- 业务需要长期演进
- 最后   - > 没有银弹。

### 微服务 集成与部署



# Docker

Docker是一个开源的引擎，可以轻松的为任何应用创建一个轻量级的、可移植的、
自给自足的容器。开发者在笔记本上编译测试通过的容器可以批量地在生产环境中
部署，包括VMs（虚拟机）、bare metal、OpenStack 集群和其他的基础应用平台。
Docker通常用于如下场景：

- web应用的自动化打包和发布；
- 自动化测试和持续集成、发布；
- 在服务型环境中部署和调整数据库或其他的后台应用；
- 从头编译或者扩展现有的OpenShift或Cloud Foundry平台来搭建自己的PaaS环境



## Docker VS VM

VM：

- 运行在宿主机之上的完整的操作系统
- 运行自身操作系统会占用较多的资源

Docker：

- Docker更加轻量高效
- 对系统资源的利用率很高
- 比虚拟机技术更为轻便、快捷
- 隔离效果不如VM



## Docker的相关概念

Docker是CS架构，主要有两个概念：
Docker daemon:

- 运行在宿主机上
- Docker守护进程
  用户通过Docker client(Docker命令)与Docker daemon交互

Docker client:

- Docker 命令行工具，是用户使用Docker的主要方式
- Docker client与Docker daemon通信并将结果返回给用户
- Docker client也可以通过socket或者RESTful api访问远程的
- Docker daemon





## 安装与hello world

## 常用命令和 docker file

## Docker Hub

里面有很多配好的环境



## 实战：打包一个web服务器