# spingcloud服务注册中心 

## 1. 使用spring boot initializer获取maven项目，http://start.spring.io/
###　Ａ．组建选择如下：

![](https://raw.githubusercontent.com/lk6678979/lk-spring-eureka-server/master/lk-eureka-server/readme/iochoose.png)  

###　Ｂ．创建完后的工程的pom.xml文件依赖如下：
```
<dependency>
	<groupId>org.springframework.cloud</groupId>
	<artifactId>spring-cloud-starter-eureka-server</artifactId>
</dependency>
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-test</artifactId>
	<scope>test</scope>
</dependency>
```

## 2.启动一个服务注册中心，需要在springboot工程的启动application类上添加@EnableEurekaServer注解：
