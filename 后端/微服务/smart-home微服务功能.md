# smart-home-auth-server

* 模块名：用户认证授权
* 功能：进行用户登录、注册、授权token、认证用户权限角色
* 应用：可以部署到居家、社区及养老机构系统平台

# smart-home-eureka-server

* 模块名：服务注册中心
* 功能：所有微服务都需要在该服务中心进行注册
* 应用：微服务必要模块

# smart-home-zuul-gateway

* 模块名：统一网关服务
* 功能：所有外部资源访问api接口，都通过统一网关进行统一路由转发
* 应用：微服务必要模块

# smart-home-common

* 模块名：公共模块
* 功能：公共的数据、常量资源、实体类
* 应用：微服务公共模块

# smart-home-redis

* 模块名：数据库缓存模块
* 功能：为了实现数据库缓存机制
* 应用：微服务公共模块

# smart-home-swagger2

* 模块名：swagger服务模块
* 功能：实现前后端交互接口api的说明文档生成
* 应用：微服务公共模块

# smart-home-bedroom-server

* 模块名：卧室模块

* 功能：进行卧室相关睡眠监测、电灯数据等信息展示及分析

* 调用子服务及公共方法：

```markdown
smart-home-bedroom-common
smart-home-mattress-sensor-service
```

* 应用：可以部署到居家、社区养老机构系统平台

# smart-home-device-server

* 模块名：设备数据存储模块
* 功能：进行所有硬件设备存储功能
* 调用子服务及公共方法

```
smart-home-device-common
smart-home-door-contact-service
.........
```

* 应用：部署到不同的平台系统中

# smart-home-gps-server

* 模块名：gps吊坠信息
* 功能：进行和吊坠gps相关的查询及操作服务
* 调用子服务及公共方法：

```
smart-home-gps-common
smart-home-gps-service
.......
```

* 应用：部署到居家、社区养老机构系统平台



