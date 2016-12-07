---
layout: single
title: About monitoring
tags: [monitoring]
date: 2013-07-26 09:50
---

WARNING: 刚刚关注，一些地方理解不完善，算是给出一些思路，需要使用者详细了解各个优缺点

## New Relic

New Relic is the all-in-one web application performance tool that lets you see performance from the end user experience down to the line of application code.

用于监控服务器状态，及自定义服务的负载，一个网站或应用相关的所有东西都可监控
    
收费并且不便宜
    
## 自己构建

对于服务异常，我们使用 [django-sentry](http://sentry.readthedocs.org/en/latest/)，相关文档及 client 比较完善
	
对于系统级监控，指标收集使用 collectd
	
对于自定义监控，指标收集使用 statsite

指标收集也可以看看：[bucky](https://github.com/cloudant/bucky)
	
对于指标展示，使用 graphite，更好的 dashboard [graphene](https://github.com/jondot/graphene) [dashing](http://shopify.github.io/dashing/)
	
对于报警，我们使用 nagios，比较灵活
	
### REFs:

[newrelic](https://newrelic.com/docs)

[http://blog.dccmx.com/2012/12/build-perfect-monitoring-system/](http://blog.dccmx.com/2012/12/build-perfect-monitoring-system/)