---
layout: single
title: Python development and production
tags: [python, development, production, vitrualenv, pythonbrew]
date: 2013-06-05 12:55
---

因为 Python 作为系统的基础库，经常被用到在很多系统或第三方软件中

为了不让开发环境污染到系统环境，这里我们推荐几种构建 Python 虚拟环境的方法

## Development

这里是指你的本地开发环境

### 1. Virtualenv

Virtualenv 是 Python 开发常用的工具之一，他可以帮助开发者针对不同项目建立独立的 Python 环境

开发者可以在这个独立的环境中，安装各种库，并且不会影响到其他项目和系统环境
    
在项目目录中运行

    virtualenv project1
    cd project1
    source bin/activate 

即可将当前环境切换为此项目的 Python 环境

安装及使用方法见：https://pypi.python.org/pypi/virtualenv
    
Virtualenv 的扩展：Virtualenvwrapper

使管理及使用更具方便

安装及使用方法见：http://virtualenvwrapper.readthedocs.org/en/latest/index.html

### 2. Pythonbrew

这是一个更强大的虚拟环境构建工具，默认他会根据 Python 的版本不同，在 $HOME 下构建各种各样的版本，并且切换相当简单

    pythonbrew install 2.7.2
    pythonbrew switch 2.7.2

它整合了 Virtualenv，更提供了类似 Virtualenvwrapper 的功能

也提供了对 Buildout 的支持，这个后面会说到
    
安装及使用方法详见：https://github.com/utahta/pythonbrew

## Production

### Buildout

他是一个神器，神奇在于一键可构建线上运行环境，大大减少了服务部署的成本

官方描述如下：

Buildout is a Python-based build system for creating, assembling and deploying applications from multiple parts, some of which may be non-Python-based. It lets you create a buildout configuration and reproduce the same software later.

1. 下载需要的脚本文件 wget http://downloads.buildout.org/1/bootstrap.py 至项目目录，并运行 python bootstrap.py
2. 修改生成的 buildout.cfg 文件，及完善项目的 setup.py 文件
3. 运行 bin/buildout, done!

现在的项目即是可以直接运行的线上服务了

第二部涉及的配置较多，他的强大之处也在这里，详见此实例：http://www.worldhello.net/2010/12/10/2207.html

官方主页：http://www.buildout.org/
