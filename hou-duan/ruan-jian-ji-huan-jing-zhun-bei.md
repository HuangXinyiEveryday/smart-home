# 一、Java for mac安装配置指南

## 1 安装软件

1.jdk—java运行环境

2.IntelliJ IDEA—java IDE集成开发软件

2.tomcat—web应用服务器（Apache服务器的扩展）

## 2 安装步骤（以mac电脑为例）

1.jdk官网下载[http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

2.IntelliJ IDEA-mac破解博客[http://www.sdifen.com/intellijidea15.html](http://www.sdifen.com/intellijidea15.html)

3.tomcat 下载地址[https://tomcat.apache.org](https://tomcat.apache.org)

下载后，通过mac电脑文件夹前往usr/local文件夹，将解压后的tomcat拷贝到该文件夹下

注：tomcat就是一个压缩文件，只需要拷贝到对应目录文件夹下即可

# 二、springboot测试小实例

Springboot本身没有代码生成也不需要xml配置，只需要run就可以创建一个独立的、产品级别的spring应用。

Springboot可以和java的开发工具（例如eclipse、intellij）也可以独立命令行使用，springboot和其他java库一样，只需要在classpath引入适当的spring-boot-\*.jar文件，就可以像java一样运行，但一般建议springboot结合maven或gradle构建工具。

## 1 使用idea新建Maven项目，修改pom.xml

Maven的核心是pom.xml，在pom.xml里可以配置Springboot以来

```xml
<!--Springboot依赖使用的groupid为org.springframework.boot-->
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>1.5.1.RELEASE</version>
</parent>
<!--Spring-boot-starter-web提供web应用依赖-->
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```

```markdown
这时Maven pom文件会继承spring-boot-starter-parent工程，声明一个或多个Starter poms依赖，所以在parent里面进行配置
parent节点使用spring-boot-starter-parent
这是一个特殊的starter，提供了有用的Maven默认设置，同时提供了dependency-management节点
```

## 2 新增具体.java代码

在src/main/java新建一个java文件

```java
package controller; /**
 * Created by Song on 2017/2/15.
 * 官方示例工程中的测试代码
 */
import org.springframework.boot.*;
import org.springframework.boot.autoconfigure.*;
import org.springframework.stereotype.*;
import org.springframework.web.bind.annotation.*;
@Controller
@EnableAutoConfiguration
public class testcontroller {
    @RequestMapping("/")
    @ResponseBody
    String home() {
        return "Hello World,this is a springboot test";
    }

    public static void main(String[] args) throws Exception {
        SpringApplication.run(testcontroller.class, args);
    }
}
```



