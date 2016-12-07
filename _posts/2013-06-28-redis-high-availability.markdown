---
layout: single
title: Redis high availability
tags: [redis, haproxy, high availability, jondis]
date: 2013-06-28 18:50
---

由于 Redis 本身不提供高可用，我们只能寻找其他方案啦

## HAProxy

HAProxy 应该是 TCP 层最简单、可靠的的高可用及负载均衡方案了

由于是服务端方案，大大提高了了客户端使用的方便性

但是对于 Redis 的高可用不适合，Redis 的单次存取都在毫秒级，而 HAProxy 的一次转发消耗也在毫秒级，直接导致了 redis 性能减半

这对单进程、单线程的 Redis server 是致命的

## Jondis

Jondis is a high availability pool management class for the excellent https://github.com/andymccurdy/redis-py

这是一个客户端方案，通过配置多个 Redis server 组成一个 Pool，这里的 Pool 并不是作为连接池来使用，其主要作为主从发现及故障转移之用

使用方式如下

    from jondis.pool import Pool
    pool = Pool(hosts=["redis01:6379","redis02:6379"])
    redis = redis_lib.client.StrictRedis(connection_pool=pool)

它会按顺序选择一个可用的 Redis server 进行连接，并执行命令，并在当前连接出错时重新选择

这种方案对 Redis server 来说是直连的，不损耗性能
