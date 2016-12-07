---
layout: single
title: Remote Control
tags: [raspberrypi, 315mhz, lamp, remote-control]
date: 2013-04-25 00:00
---
![BOARD](/photos/board.jpg)

所需硬件：

[树莓派](http://www.raspberrypi.org/)一块

[315mhz 模块](http://s.taobao.com/search?initiative_id=staobaoz_20130425&jc=1&q=315m+%C4%A3%BF%E9) 发射、接受模块一组
    
[遥控灯头](http://s.taobao.com/search?initiative_id=staobaoz_20130425&jc=1&q=%D2%A3%BF%D8%B5%C6%CD%B7) 一组
    
所需软件：

[rcswitch-pi](https://github.com/iamsk/rcswitch-pi)

[wiringpi](https://projects.drogon.net/raspberry-pi/wiringpi/download-and-install/)

电路连线如上图：

上图左边为 315 模块发射端，用于替代原遥控器，并可结合树莓派，进行远程控制

上图右边为 315 模块接收端，用于监测原遥控器的发射的地址码，当然可以直接去查看遥控器电路

如图：

![BOARD](/photos/rc.jpg)

此处我们用的是灯的遥控器，对应的的地址码为：10FF0110，从右向左查看，上 1 下 0 置空 为 F

我们去掉 315Mhz 接收端，留下发送端即可

初始状态为关闭，如图

![CLOSE](/photos/close.jpg)

执行命令（sudo ./send.out 10FF0110 1）后，如图，灯亮了

![OPEN](/photos/open.jpg)

使用任何语言在树莓派上写个简单的 API 接口，即可提供给手机作远程控制
