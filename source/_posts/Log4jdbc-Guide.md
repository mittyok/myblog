---
title: Log4jdbc-Guide
date: 2016-10-01 21:47:53
tags:
  - log4j
  - sql
  - tuning
  - springboot
---
> 基于Springboot 1.4

## 配置依赖
```xml
<!-- https://mvnrepository.com/artifact/org.bgee.log4jdbc-log4j2/log4jdbc-log4j2 -->
<dependency>
    <groupId>org.bgee.log4jdbc-log4j2</groupId>
    <artifactId>log4jdbc-log4j2-jdbc4.1</artifactId>
    <version>1.16</version>
</dependency>
```

## 配置驱动
```properties
spring.datasource.driver-class-name: net.sf.log4jdbc.sql.jdbcapi.DriverSpy
```

## 配置Log探测器
在classpath下建一个文件，命名为：*log4jdbc.log4j2.properties*。添加如下内容：
```properties
log4jdbc.spylogdelegator.name=net.sf.log4jdbc.log.slf4j.Slf4jSpyLogDelegator
```

OK啦，启动吧，现在应该有效果了。

**太详细的，大家再到网上看一下吧。。。**

***需要注意的一些日志配置***
Log4jdbc 用以下几个可以配置的日志种类：
```
    jdbc.sqlonly : 仅记录 SQL
    jdbc.sqltiming ：记录 SQL 以及耗时信息
    jdbc.audit ：记录除了 ResultSet 之外的所有 JDBC 调用信息，会产生大量的记录，有利于调试跟踪具体的 JDBC 问题
    jdbc.resultset ：会产生更多的记录信息，因为记录了 ResultSet 的信息
    jdbc.connection ：记录连接打开、关闭等信息，有利于调试数据库连接相关问题
```
    
配置形式可参考如下：
```
    log4j.logger.jdbc.sqlonly=OFF
    log4j.logger.jdbc.sqltiming=INFO
    log4j.logger.jdbc.audit=OFF
    log4j.logger.jdbc.resultset=OFF
    log4j.logger.jdbc.connection=OFF
```
