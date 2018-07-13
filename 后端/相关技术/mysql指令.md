#### 1.创建数据库

```
CREATE DATABASE 数据库名;
```

#### 2.显示当前数据库

```
#显示所有数据库
show databases;


#删除特定数据库
drop database 数据库名;
```

如果创建数据库名有特殊字符 例如-这种，如果mysql版本为8.\*版本，报错的话解决方法如下：

    create database `d-d`;加反引号

#### 3.执行sql脚本文件

```
source sql路径
```

注：**docker下执行sql脚本文件**

```
#1.将宿主机上的数据sql复制到容器的文件中
docker cp 本机sql路径 容器名:容器保存sql路径
例如 docker cp /Users/x/Desktop/ProjectCode/smart-home/smart-home-auth-server/Dump20180604.sql 
smarthome-mysql:/opt/Dump20180604.sql


#2.进入容器
docker exec -it 容器名 bash

#3.登录容器内的mysql数据库
mysql -uroot -p123456


#4.执行sql脚本
source 容器保存sql路径
```

#### 4.mysql下切换进入指定数据库

```
use 数据库名;
```

#### 5.mysql清空表中所有数据

```
1.truncate table 表名//自增id重新从1开始
2.delete from 表名//自增id从删除后的数据后继续增加
注：原因是delete会记录数据库日志，数据可恢复；truncate不记录日志，数据不可恢复
```

#### 6.mysql增加数据获取当前时间

```
在新增表时，可以使用如下命令表示默认时间是系统时间
使用DEFAULT CURRENT_TIMESTAMP
数据库中datatime也是timestamp类型
ADD COLUMN  `CreateTime` datetime NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间' 
```

