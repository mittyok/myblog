---
title: Schema-Generator-By-JPA
date: 2016-11-16 10:29:13
tags:
  - database
  - ddl
  - hebernate
  - eclipselink
  - jpa
---
## 配置
```lang=xml
<!-- /////// START JPA Schema Generator -->
<plugin>
    <groupId>io.github.divinespear</groupId>
    <artifactId>jpa-schema-maven-plugin</artifactId>
    <version>0.2.0</version>
    <executions>
    </executions>
    <configuration>
    <jdbcUrl>这里配置jdbcurl</jdbcUrl>
    <jdbcUser>数据库用户名</jdbcUser>
    <jdbcPassword>数据库密码</jdbcPassword>
    <!-- 这里需要指定JPA的实现提供者 -->
    <vendor>hibernate</vendor>
    <!--<databaseAction>create</databaseAction>-->
    <scriptAction>drop-and-create</scriptAction>
    <!--<scriptAction>${AAA}</scriptAction>-->
    <packageToScan>指定要扫描实体的包路径</packageToScan>
    <properties>
        <hibernate.dialect>org.hibernate.dialect.MySQL5Dialect</hibernate.dialect>
    </properties>
</configuration>
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
相关配置可以参照：[jpa-schema-plugin](http://divinespear.github.io/jpa-schema-maven-plugin/generate-mojo.html)
