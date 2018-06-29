# 一、连接服务器

```bash
ssh smarthome@192.168.85.208
//smarthome为用户名，@后为ip地址
password:smarthome
```

# 二、本地或服务器jar包部署运行

## 1.项目打包

必须在smart-home目录下

```
//可在本地打包，也可在服务器打包(使用git，保证代码最新)
mvn clean package -Dmaven.test.skip=true
```

## 2.运行jar包

* #### 服务器运行jar

进入想要运行的服务的jar包目录下， 一般会自动生成target的目录下有jar包

```bash
//使用nohup和&，当终端关闭后程序还是可以运行
nohup java -jar smart-home-gps-server-1.0-SNAPSHOT.jar&
```

* #### 本地打包上传服务器运行

上传jar包到服务器（linux上传文件到远程服务器）

```
//进入需要拷贝的文件目录下，直接拷贝文件到远程服务器tmp目录下(默认只有tmp目录下有权限)
 scp DoorContact20180625.sql smarthome@192.168.85.208:/tmp
```

注：服务器重新运行同一个服务jar包，需要使用命令kill杀死原有jar进程，才可以重新运行，否则端口被占用无法成功

```
ps -ef | grep java
sudo kill -9 <进程号>
```

# 二、docker镜像运行

## 1.项目打包（同上）

## 2.docker打包镜像

* 在自己开发的资源服务包下面新增一个Dockerfile文件（参考现有的文件）

```
FROM java:8
WORKDIR /code
#jar包一般在target目录下
COPY ./target/smart-home-auth-server-1.0-SNAPSHOT.jar /code
#需要和yml文件的端口号一致
EXPOSE 8762
CMD ["java","-jar","smart-home-auth-server-1.0-SNAPSHOT.jar"]
```

* 镜像打包需要在dockerfile所在目录下

```
$ sudo docker build -t <你的镜像名>:<tag> .
```

注：镜像名自己定义，后面的.必须要

* 打包的镜像发布到docker服务器上

```
推送到阿里云docker或docker hub，需要进行阿里云或hub注册（hub为国外服务器）

添加命名空间和仓库名
参考博客：https://blog.csdn.net/ximenghappy/article/details/66971035
https://blog.csdn.net/u013096666/article/details/76522065

```

```
登录阿里云docker
docker login registry.cn-hangzhou.aliyuncs.com
或者docker login --username=用户名 registry.cn-hangzhou.aliyuncs.com

username 为阿里云账号
password 为registery密码，初始密码为阿里云密码(可以修改)
```

```
推送镜像到registry
docker tag auth-server:8762 registry.cn-hangzhou.aliyuncs.com/命名空间/仓库名:[镜像版本号]
docker push registry.cn-hangzhou.aliyuncs.com/命名空间/仓库名:[镜像版本号]
```

```
存在问题：如果无法登录或push


更新下载osxkeychain


https://github.com/docker/docker-credential-helpers/releases 


下载后的osxkeychain解压后，双击运行后，移动到/usr/local/bin文件夹下


mac:


cd ~/Downloads


mv docker-credential-osxkeychain /usr/local/bin


chmod 555 /usr/local/bin/docker-credential-osxkeychain
```

## 3.服务器端下载镜像

* 服务器端直接下载docker镜像

```
进入服务器，输入如下命令


从registry拉取镜像


docker pull registry.cn-hangzhou.aliyuncs.com/命名空间/仓库名:[镜像版本号]
```

* 运行docker镜像

```
docker run -d --net=host --name container-name image-name
```



