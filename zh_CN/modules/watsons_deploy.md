# EMQX & Watsons SDES Deploy

## 架构设计

### EMQX Enterprise Watsons SDES 定制版本

基于 EMQX 企业版，定制开发插件，包含以下功能

- 认证：门店启动认证（基于 IP 地址颁发门店信息、认证信息），设备 BOOT 流程之后的连接管理和认证管理
- 鉴权：业务流程认证，文件传输基于 SDES Job 管理，对文件传输过程中的双端（服务器与门店）授权
- 文件传输协议：文件分片，完整性校验、文件广播、分区推送
- 协议控制：业务管理、流量控制、设备信息下发、文件传输业务下发
- 设备管理插件：门店消息通道管理，上下线即时通知

模块的开启与启动请参考 `Watsons Module` 章节。

EMQX Enterprise 版本使用三节点集群的方式，确保服务高可用。

### EMQX Backend API

使用 Java SpringBoot 框架编写的微服务，RESTFul API 。为 SDES 前端控制台提供服务。详细的 API 接口文档参考 `API docs` 章节。

### MySQL 数据库

为 SDES 平台提供数据支撑。数据库表设计参考 `MySQL DataBase` 章节。

### 前端交互组件 SDES Dashboard

#### 功能（3小节：接入、消息分发、数据缓存）

#### 规则引擎使用（只要写MySQL资源配置、日志上报持久化规则。上下线事件已经转移至插件内部实现）

## 架构图

![sdes_architecture](./assets/sdes/sdes_architecture.png)
