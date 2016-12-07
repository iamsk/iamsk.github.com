---
layout: single
title: iphone-debug-with-charles
tags: [iphone, http, charles, debug, https]
date: 2013-06-28 11:50
---

## 针对 http 的监听

下载 charles 最新版，安装并运行，默认已打开监听

charles 会在本机的 8888 端口开启代理服务

在同一局域网内，手动设置手机的 HTTP Proxy 为电脑的 IP 地址，端口为 8888

charles 监听到有请求时，会弹出授权确认按钮，确定即可

此时所有手机的 HTTP 请求将会被 charles 监听到，对于 https 的请求无法监听

## 针对 https 的监听

下载 charles [证书](/files/charles-proxy-ssl-proxying-certificate.crt)至手机并安装, 在 charles 中设置 Proxy > Proxy Settings > SSL > Enable SSL Proxying > 添加需访问的 https 链接

剩余的操作如 http 方式
