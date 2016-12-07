---
layout: post
title: TMiddleware - middleware for tornado
tags: [tornado, middleware, python]
date: 2013-05-23 23:00
---

很多场景下，使用 middleware 可以大大简化服务的流程，并降低不相关功能的耦合度

此处模仿 Django 的 middleware，编写了 middleware 的管理功能，使开发人员可以方便的编写 tornado 的 middleware 服务

## Minimal Demo

### $ more examples/mimimal.py

    import tornado
    import tornado.httpserver
    from tornado.options import define, options
    from tornado.web import RequestHandler

    from tmiddleware.handler import TMiddlewareHandler

    define('port', 7777)
    MIDDLEWARES = ['plugins.slow_request.SlowRequestMiddleware', 'plugins.profile.ProfileMiddleware']
    define("middlewares", default=MIDDLEWARES, help="middleware class list")


    class With(TMiddlewareHandler):
        def get(self):
            import time
            time.sleep(4)
            return self.finish('Hello World!')


    def run():
        application = tornado.web.Application([('/', With)])
        http_server = tornado.httpserver.HTTPServer(application, xheaders=True)
        http_server.listen(options.port, '0.0.0.0')
        tornado.ioloop.IOLoop.instance().start()

    if __name__ == '__main__':
        run()

此处使用了自带的两个 middleware，一个用于查看请求的 profile 信息，一个用于在终端下记录超时的请求

### $ python mimimal.py

### $ chrome http://localhost:7777/?__profile__=true

Web

![TMiddleware-web](/photos/tmiddleware-web.jpg)

Console

![TMiddleware-console](/photos/tmiddleware-console.jpg)

## Plugins

自带了两个：

1. profile: 查看请求的内部函数耗时信息
2. slow_request: 记录超时请求

自定义插件参考这两个即可

Github: [iamsk/tmiddleware](https://github.com/iamsk/tmiddleware)
