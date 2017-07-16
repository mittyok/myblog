---
title: Hazelcast_Jcache_Implementation
date: 2016-11-14 10:43:44
tags:
  - hazelcast
  - spring cloud
  - jcache
---

## 加入JCache依赖
```
<dependency>
  <groupId>javax.cache</groupId>
  <artifactId>cache-api</artifactId>
  <version>1.0.0</version>
</dependency>
```

## 加入Hazelcast依赖
1. If hazelcast-\<version>.jar is added to the classpath, Hazelcast can only be used as a server provider.
2. If hazelcast-client-\<version>.jar is added to the classpath, default provider is the client one.
3. If hazelcast-all-\<version>.jar is added to the classpath, default provider is again the client one.