# 一、准备工作

Java、Maven、SpringBoot、SpringCloud、Docker、Git

# 二、SmartHome功能架构

![](/assets/屏幕快照 2018-06-29 下午2.07.46.png)

# 三、SmartHome物理结构

![](/assets/屏幕快照 2018-06-29 下午2.11.56.png)

# 四、SmartHome技术栈选型

## 1.SmartHome架构说明

* App、Web和微信端实现前后端分离技术

* 前端使用Vue+Webpack+ngix技术

* 服务端使用SpringCloud技术栈实现微服务架构

* 微服务之间使用redis+mysql做消息100%可达，保证微服务持久化（redis缓存还可以提高消息吞吐量）

* 统一网关API使用基于OAuth2.0的安全认证，app、web及微信使用基于JWT的安全认证

* 目前每个独立的微服务使用java（基于SpringBoot）构建工程

* 使用客户的负载均衡Ribbon从服务注册中心（Eureka）拉取服务列表，根据业务特点加权负载调用

* 使用Hystrix做服务熔断/降级处理，避免单个微服务不可用引起整个系统崩溃，提高系统可用程度

* 使用Boot admin做服务监控指标

* 使用Feign做服务内部之间调用

* 使用阿里云短信服务，进行第三方短信平台发送；使用百度API接口

## 2.SmartHome技术选型

SpringBoot——基础构建框架，用于快速整合资源

SpringFramework——底层容器

SpringCloud——微服务框架

SpringCloudEureka——微服务注册中心

SpringCloudZuul——微服务网关

SpringCloudHystrix——微服务容错框架

SpringCloudFeign——微服务声明式调用框架

SpringBootAdmin——微服务管理中心

SpringDataJpa——微服务持久化框架

SpringDataRedis——缓存框架

Oauth2.0——安全框架

SpringValidator——后端验证框架

Maven——项目构建管理

Redis——分布式缓存数据库

Mysql——对象关系数据库

CAS——单点登录认证

## 3.SmartHome技术栈

* 前端

  VUE.js

* 服务端（JAVA）

  SpringCloud、Zuul（统一网关）、Feign（微服务之间通信）

  Hystrix（超时熔断）、Turbine（汇总系统内多个服务的数据）、Eureka（服务注册）

  Ribbon\(负载均衡\)、BootAdmin（服务监控）、Zipkin（调用链监控）

  OAuht2（安全认证）、JWT（前端安全认证）、Hibernate/Mybatis（持久层框架）

  Mapper3、PageHelper、Security

  Mysql\(数据库）、Redis（数据库功能））、,MQ（消息服务）

  zookeeper（分布式协调服务）、elastic-job（分布式定时任务框架）、mail（邮件服务）

* 第三方服务

  阿里云短信服务

  百度地图API

# 五、SmartHome项目模块划分

## 1.服务管理模块—smarthome\_sm

* smarthome\_sm\_admin:系统管理后台

* smarthome\_sm\_api:系统服务对外接口

* smarthome\_sm\_api\_feign:基于Spring Cloud Feign的调用实现

* smarthome\_sm\_core:系统管理核心

* smarthome\_sm\_server:系统管理服务

## 2.配置模块—smarthome\_configuration

## 3.用户登录模块—smarthome\_usrlogin

* smarthome\_usrlogin\_client 客户端jar包，用于集成到需要CAS授权的系统

* smarthome\_usrlogin\_server CAS服务端，单独部署，用于完成用户的登录，进入主界面功能

* smarthome\_usrlogin\_manager CAS服务管理，用于管理授权服务等

## 4.公共模块—smarthome\_common

* smarthome\_common\_api:前后端数据传输公共接口，实现后端数据传输给前端

* smarthome\_common\_getdata:数据库读取数据公共模块，实现从数据库取数据

## 5.接口模块—smarthome\_api

* smarthome\_api\_kitchen:厨房接口

* smarthome\_api\_livingroom:卧室接口

* smarthome\_api\_sleep:睡眠接口

* smarthome\_api\_bathroom:卫生间接口

* smarthome\_api\_healthy:生理指标接口

* smarthome\_api\_danger：危险隐患接口

* smarthome\_api\_notification：物品报警接口

* smarthome\_api\_abnormal：异常指标接口

* smarthome\_api\_healthyreport：健康报告接口

* smarthome\_api\_gps：gps数据接口

## 6.居家养老模块—smarthome\_jjyl

* smarthome\_jjyl\_usercenter：居家养老用户中心

* smarthome\_jjyl\_backmanager：居家养老后台管理

* smarthome\_jjyl\_fridgesensor：冰箱传感器数据处理

* smarthome\_jjyl\_gassensor：燃气传感器数据处理

* smarthome\_jjyl\_dietsensor：饮食传感器数据处理

* smarthome\_jjyl\_lamp:电灯数据处理（包括卧室、厨房、客厅、卫生间等）

* smarthome\_jjyl\_mattresssensor：床垫传感器数据处理（包括睡眠、翻身、心率等信息）

* smarthome\_jjyl\_sofasensor：沙发传感器数据处理

* smarthome\_jjyl\_aircondition：空调数据处理

* smarthome\_jjyl\_tv：电视数据处理

* smarthome\_jjyl\_stoolsensor：马桶传感器数据处理

* smarthome\_jjyl\_washsensor：洗澡传感器数据处理

* smarthome\_jjyl\_hydrovalvesensor：水阀传感器数据处理

* smarthome\_jjyl\_sos：sos呼救处理

* smarthome\_jjyl\_tumblesensor：跌到检测传感器数据处理

* smarthome\_jjyl\_notificationsensor：物品忘带提醒传感器数据处理

* smarthome\_jjyl\_gps:gps定位数据

* smarthome\_jjyl\_bloodglucose：血糖数据处理

* smarthome\_jjyl\_bloodpressure：血压数据处理

* smarthome\_jjyl\_temperature：体温数据处理

* smarthome\_jjyl\_heartrate：心率数据处理

* smarthome\_jjyl\_bmi：bmi数据处理

* smarthome\_jjyl\_medicinebox：药盒数据处理

* smarthome\_jjyl\_devicecontrol：设备控制

---

## 7.养老机构模块—smarthome\_yljg

后期更新

## 8.大数据平台分析模块—smarthome\_datacenter

后期更新

## 9.消息推送模块—smarthome\_notification

用来推送到app、web及微信小程序端日常消息、异常报警、系统分析等信息

## 10.支付模块—smarthome\_pay

用来提供支付功能，调用第三方平台支付接口（支付宝、微信）

## 11.数据处理行为分析模块—smarthome\_machinelearning

对不同模块采用机器学习的方式进行数据处理及行为分析，主要分为两个部分

* 单独模块及传感器的数据处理分析

* 综合老人各项指标数据（包括历史数据）进行行为分析等

```
注：7、8另外两个需要开发的系统


 9、10为后期需要开发的服务模块


 11是机器学习核心模块
```

## 12.设备数据采集模块—smarthome\_datacollect

涉及将硬件数据采集到数据库，后期使用模块化、可视化方式进行开发

_**注:后一阶段工作**（涉及具体设计工作）_

## 13.工作流模块—smarthome\_bpm

用来对不同微服务进行工作流程、步骤及逻辑的串联，保证系统获取有效信息，实现功能

**注：主要是用来实现后台工作流串联（后期可以使用可视化的方式进行编程开发）**

## 14.内容管理模块—smarthome\_cms

前端网站开发模块，用来加速网站开发，通过提供大量固定的模板减少开发人员开发时间，即使用可视化的方式辅助开发人员进行前端网站的开发。

_**注：后期拓展**_

```
12/13/14是开发可视化、流程化的拓展辅助，有助于后期开发，因此优先级最后
```



