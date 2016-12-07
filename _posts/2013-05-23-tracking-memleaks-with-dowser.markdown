---
layout: post
title: Tracking memory leaks with dowser
tags: [memory, leak, dowser, python, tornado, django]
date: 2013-05-23 21:40
---

## Dowser in tornado

Dowser is a CherryPy application that displays sparklines of Python object counts, and allows you to trace their referents. This helps you track memory usage and leaks in any Python program, but especially CherryPy sites.

And CherryPy is WSGI enabled.

Tornado 默认的 http server 是非 wsgi 协议的，所以需要用其 WSGIContainer 进行转换

    import dowser
    import cherrypy
    from tornado.wsgi import WSGIContainer

    dowser_app = WSGIContainer(cherrypy.tree.mount(dowser.Root(), '/_dowser'))
    handlers.insert(0, (r'/_dowser.*', tornado.web.FallbackHandler, dict(fallback=dowser_app)))

后两句用于将一个 wsgi 的应用运行于 tornado http server

自此即可在 http://domain:port/_dowser 进行查看各个对象引用数及增长状况等信息

## Dowser in django

有现成的 app 可用：https://github.com/munhitsu/django-dowser

Refs:

http://www.aminus.net/wiki/Dowser

https://groups.google.com/forum/#!msg/python-tornado/D4kSwHg5da0/d_3Dz3QZ4OIJ

http://www.tornadoweb.org/en/stable/wsgi.html

http://wsgi.readthedocs.org/en/latest/frameworks.html
