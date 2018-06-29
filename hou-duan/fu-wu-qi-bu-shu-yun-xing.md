1.新增服务，xml中的select语句必须配置 resultType，否则会报错

```
Request processing failed; nested exception is org.mybatis.spring.MyBatisSystemException: nested exception is org.apache.ibatis.executor.ExecutorException: A query was run and no Result Maps were found for the Mapped Statement 'cn.edu.chzu.smart.home.dao.UserDeviceMappingDao.findDeviceBySn'.  It's likely that neither a Result Type nor a Result Map was specified.] with root cause
```

2.服务之间调用报错

```
"com.netflix.client.ClientException: Load balancer does not have available server for client: smart-home-device-mapping-service"
```

解决：

* 查看主服务和子服务是否引入依赖

* 查看主服务FeignClient的服务名和子服务application.yml服务名是否相同

  


