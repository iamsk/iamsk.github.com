---
layout: single
title: Autoreload in tornado, gunicorn, supervisor, etc
tags: [tornado, autoreload, gunicorn, supervisor]
date: 2013-05-27 22:10
---

## Tornado

### 1. tornado.autoreload

    import tornado.autoreload

    instance = tornado.ioloop.IOLoop.instance()
    tornado.autoreload.start(instance)
    instance.start()

### 2. debug in settings

    application = tornado.web.Application([(r"/", DemoHandler)], debug=True)

Tornado 默认每 0.5s 通过监测 python 文件的变化进行自动重启, 建议只将这种方式用于开发模式，生产环境请勿使用

## Gunicorn

### 1. max_requests

单个 worker 当最大请求数达到 max_requests 时，将触发重启行为，这种行为可以减少内存泄漏引起的错误

### 2. timeout

官方文档中是这么说的: Workers silent for more than this many seconds are killed and restarted.
    
由于 gunicorn 的 worker 和 master 是以 Notify 的方式进行管理的，当 timeout 内没有通知 master，则 worker 会被 master 干掉

在 web 服务中也就是当请求超过 timeout(default 30s) 时，会自动重启对应 worker

Gunicron 的这种运行方式，对服务的稳定性是友好的，但会隐藏程序中的一些问题，并且可能会在你更新代码后，它由于以上原因而重启引发问题

## Supervisor

用于管理进程，并且可配置在进程挂掉时是否自动重启，包括只要挂了就重启及只有对应的结束返回值才会重启等策略

Refs:

https://github.com/facebook/tornado/blob/master/tornado/autoreload.py

http://docs.gunicorn.org/en/latest/configure.html

http://supervisord.org/
