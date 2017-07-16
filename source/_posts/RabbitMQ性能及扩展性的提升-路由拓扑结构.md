---
title: RabbitMQ性能及扩展性的提升-路由拓扑结构
date: 2016-12-28 14:48:15
tags:
  - rabbitmq
  - performance
  - routing
  - scalability
---
> [原文](https://spring.io/blog/2011/04/01/routing-topologies-for-performance-and-scalability-with-rabbitmq/)

为了实现系统的高伸缩性，我们需要设计一个合适的路由拓扑。我们需要考虑很多的细节，比如：消息实现环境中存在的问题及限制，性能策略等。