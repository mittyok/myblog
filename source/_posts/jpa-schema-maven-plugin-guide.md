---
title: jpa-schema-maven-plugin_guide
date: 2016-10-01 15:19:50
categories:
  - maven
  - ddl
tags:
  - maven
  - hibernate
  - ddl
  - schema
comments: true
---
# 配置
```xml
<!-- /////// START JPA Schema Generator -->
<plugin>
    <groupId>io.github.divinespear</groupId>
    <artifactId>jpa-schema-maven-plugin</artifactId>
    <version>0.2.0</version>
    <configuration>
        <jdbcUrl>jdbc:mysql://192.168.99.100:3306/dawnorder</jdbcUrl>
        <jdbcUser>root</jdbcUser>
        <jdbcPassword>dawn12345678</jdbcPassword>
        <vendor>hibernate</vendor>
        <!--<databaseAction>create</databaseAction>-->
        <scriptAction>drop-and-create</scriptAction>
        <!--<scriptAction>${AAA}</scriptAction>-->
        <packageToScan>com.huobi.dawn.common.entity</packageToScan>
        <properties>
            <hibernate.dialect>org.hibernate.dialect.MySQL5Dialect</hibernate.dialect>
        </properties>
    </configuration>
    <executions>
    </executions>
    <dependencies>
        <!-- https://mvnrepository.com/artifact/org.eclipse.persistence/eclipselink -->
        <dependency>
            <groupId>org.eclipse.persistence</groupId>
            <artifactId>eclipselink</artifactId>
            <version>2.6.4</version>
        </dependency>
        <dependency>
            <groupId>org.hibernate</groupId>
            <artifactId>hibernate-core</artifactId>
            <version>5.0.9.Final</version>
        </dependency>
        <dependency>
            <groupId>org.hibernate</groupId>
            <artifactId>hibernate-entitymanager</artifactId>
            <version>5.0.9.Final</version>
        </dependency>
        <dependency>
            <groupId>org.hibernate.javax.persistence</groupId>
            <artifactId>hibernate-jpa-2.1-api</artifactId>
            <version>1.0.0.Final</version>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.39</version>
        </dependency>
    </dependencies>
</plugin>
<!-- JPA Schema Generator END ///////// -->
```
# 执行
> mvn jpa-schema:generate
