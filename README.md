# spingcloud服务注册中心 

## 1. 使用spring boot initializer获取maven项目，http://start.spring.io/
### 1.1 组建选择如下：

![](https://raw.githubusercontent.com/lk6678979/lk-spring-eureka-server/master/lk-eureka-server/readme/iochoose.png)  

### 1.2 创建完的工程pom.xml文件中的依赖如下：

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

## 2.代码编写
### 2.1 JAVA代码，仅需要在springboot工程的启动application类上添加`@EnableEurekaServer`注解：
```
@SpringBootApplication
@EnableEurekaServer
public class EurekaServerApplication {

	public static void main(String[] args) {
		SpringApplication.run(EurekaServerApplication.class, args);
	}
}
```
### 2.2 创建3个配置文件，applycation-one.yml,applycation-two.yml,applycation-three.yml(用于注册中心高可用集群)，其中一个配置文件如下
```
#服务启动端口号
server:
  port: 8806

spring:
  profiles: one

eureka:
  instance:
    #设置当前实例的主机名称
    hostname: eureka.server.one
  client:
    #是否启动服务注册
    registerWithEureka: false
    #是否检索服务
    fetchRegistry: false
    #指定服务注册中心地址，这里使用3个注册中心相互注册实现集群
    serviceUrl:
      defaultZone: http://eureka.server.three:8808/eureka/,http://eureka.server.two:8807/eureka/
```
### 2.3 启动
#### 2.3.1 使用maven打包项目
#### 2.3.2 启动jar
依次执行下面指令启动3个集群的注册中心：  
	java -jar lk-eureka-server-0.0.1-SNAPSHOT.jar --spring.profiles.active=one  
	java -jar lk-eureka-server-0.0.1-SNAPSHOT.jar --spring.profiles.active=two  
	java -jar lk-eureka-server-0.0.1-SNAPSHOT.jar --spring.profiles.active=three


	
