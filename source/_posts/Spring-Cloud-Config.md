---
title: Spring Cloud -- Config
date: 2016-11-13 15:58:57
tags: 
  - spring cloud
  - config server
  - config client
---

## 什么是Spring Cloud Config
Config主要是为了解决分布式应用中的配置管理问题。Spring Cloud Config对配置进行集中化管理，提供了Server端和Client端的解决方案。所有的应用和服务都可以通过Server端管理、访问自己的配置。而且，Server端的配置我们还可以通过`版本管理工具`管理起来。

## 为什么需要Config

曾几何时，我们把配置直接硬编码到我们的代码中，中途我们发现，配置一遍，我们就要改代码，重新构建工程，重新部署。于是我们聪明了一些，把配置写到配置文件中，这样不用改代码了，不用重新构建工程，但是依然不是那么愉快，我们还是要重新部署应用来使新的配置生效。好吧，我姑且接受这个现实吧。。。

突然有一天，我们发现，为了应对日益增长的访问量，一不小心，一盒应用我们部署了很多实例。。。别太美，我们发现改配置的话好麻烦啊，因为每一个实例中对应的配置都要修改，重新打包，重启。。。

突然，背后一阵凉风。。。ʘ‿ʘ

多么希望能有一个统一的地方用来管理配置。。。暂时就这么点需求。

好吧，Spring Cloud Config来满足你。

## 简单搭建一个Config Server
1. 打开[SPRING INITIALIZR](https://start.spring.io/)
![](http://ogj4ygzvp.bkt.clouddn.com/SPRING%20INITIALIZR%20.png)
2. 添加了Config Server的依赖
3. 点击：Generate Project
4. 解压产生的项目，看一下项目结构：
![](http://ogj4ygzvp.bkt.clouddn.com/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202016-11-13%20%E4%B8%8B%E5%8D%885.15.31.png)
4. 编辑DemoApplication.java,划线的地方是新加入的
![](http://ogj4ygzvp.bkt.clouddn.com/config%20server%20enable.png)
4. resources下加入：bootstrap.yml
- 配置config server使用本地配置提供服务，具体配置如下：
![](http://ogj4ygzvp.bkt.clouddn.com/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202016-11-13%20%E4%B8%8B%E5%8D%887.15.42.png)
4. resources下加入`conf`文件夹，建立application.yml文件，加入如下内容：

```
application:
  name: mittyok-test
```
5. 在目录下执行：`./mvnw package`
6. 到`target`目录下面
7. ![](http://ogj4ygzvp.bkt.clouddn.com/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202016-11-13%20%E4%B8%8B%E5%8D%885.28.42.png)
8. 执行命令<br>`java -jar demo-0.0.1-SNAPSHOT.jar`<br>
我们等待着。。。
![](http://ogj4ygzvp.bkt.clouddn.com/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202016-11-13%20%E4%B8%8B%E5%8D%885.31.48.png)
看到上面这个输出，应该已经启动OK。

## 验证Config Server OK
我们上面在conf中只放入了一个application.yml文件，这个文件的配置会默认对所有应用有效，我们看一下刚才我们的配置是否被Config Server读取：

访问：`http://localhost:8080/application-defualt.yml`
如果能看到如下结果，说明Server已经启动成功啦：

![](http://ogj4ygzvp.bkt.clouddn.com/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202016-11-13%20%E4%B8%8B%E5%8D%887.32.28.png)

## 搭建一个简单的Config Client

## Config监控
有时候我们需要在修改配置后，相关的客户端要refresh，重新加载配置。这个时候，我们需要用到Spring 
Cloud Bus, Bus负责将Config Server端的事件广播到对应的应用，使应用重新加载配置。

- 假设，我们我们通过rabbit作为消息中间件，bus的事件广播渠道，则Config Server端我们需要如下配置：

	**pom.xml**

```xml
	<!-- 通过此消息中间件广播 -->
	<dependency>
	    <groupId>org.springframework.cloud</groupId>
	    <artifactId>spring-cloud-starter-stream-rabbit</artifactId>
	    <version>1.0.2.RELEASE</version>
	</dependency>
	<!-- 事件总线，监听及处理cloud中的一些事件，如通过/monitor传入的操作 -->
	<dependency>
	    <groupId>org.springframework.cloud</groupId>
	    <artifactId>spring-cloud-bus</artifactId>
	</dependency>
	<!-- 使服务暴露/monitor endpoint 以方便外部触发监听事件 -->
	<dependency>
	    <groupId>org.springframework.cloud</groupId>
	    <artifactId>spring-cloud-config-monitor</artifactId>
	    <version>1.1.2.RELEASE</version>
	</dependency>
```
**bootstrap.yml**

```yml
spring:
  rabbitmq:
    addresses: 192.168.99.100:5672 # rabbitmq地址
    username: admin # 用户名
    password: admin # 密码
```

- Config Client端与服务端配置基本一致，但是不需要暴露/monitor endpoint

>> *注意：*两端的事件实体与Json的转换规则上一定要一致，不要出现客户端转化成的json使用hyphon格式（"`-`"），而服务端用camelcase的形式读取，类似这样的问题。


## 待续