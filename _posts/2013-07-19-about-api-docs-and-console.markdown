---
layout: single
title: about-api-docs-and-console
tags: [api, doc, console]
date: 2013-07-19 23:50
---

API 开发的功能是核心，但对开发者友好的文档及可调式的控制台则必不可少，这个关系着开发效率，沟通以及可维护性

原先在知乎开发时，文档经历了 task 的附加信息，Markdown，Sphinx等等

总得来说，手动编写的内容过多，并且需要重复很多冗余信息

而对于用于调试的控制台，自己构建了一个，认为还是比较方便的

关于这两方面，其实已有现成的工具可以解决

## [swagger](https://developers.helloreverb.com/swagger/)

Swagger 是一个规范，并且作为一个框架它完整实现了通过代码生成漂亮的在线 API，并且可以直接模拟运行，也就是说提供了控制台功能

[Wiki](https://github.com/wordnik/swagger-core/wiki) 里有详细的说明

[Demo](http://petstore.swagger.wordnik.com/) 效果非常棒的，第一眼应该就会喜欢上它

查看了 Python 的两个实现：[Django](https://github.com/marcgibbons/django-rest-swagger) 和 [django-tastypie-swagger](https://github.com/concentricsky/django-tastypie-swagger)

优点是随着 API 的实现，同步的更新；

缺点是和 API 耦合性较大，属于同一个 repo，再一个是必须以他的规范来写，对于旧的项目不太合适，针对使用以上框架的新项目倒是非常合适的

django-tastypie + django-tastypie-swagger or django-rest-framework + django-rest-swagger 都是不错的选择

不过自从用了 Tornado 之后，再也无法忍受 Django 这样的框架了，而针对 Tornado 写个 swagger 插件还是挺麻烦的，而且不够灵活

## [I/O Docs](https://github.com/mashery/iodocs)

功能和 swagger 类似，但无耦合性，所有的文档及控制台，均是基于配置文件的，从灵活性与低的耦合性来看，还是比较推荐的，不过界面不够漂亮，基于 nodejs，遇到坑的话，不能很快的解决

[Demo](http://developer.mashery.com/iodocs)

## [restdown](https://github.com/trentm/restdown)

这个不同于以上两点的是，它只提供文档功能，不提供控制台功能

通过试用发现他的依赖很小，并且是基于 markdown 的，所以非常喜欢，功能简单，灵活，针对可能产生冗余的文档编写，我们可以通过脚本自动根据我们的 handler 生产 markdwon 文件，并且针对各个框架是灵活的，比如我写的 RESTFul API 框架 [Brat](https://github.com/iamsk/brat) 就是这样的方式

## 其他

还有一些其他的可在 [tools-to-generate-beautiful-api-documentation](http://www.mattsilverman.com/2013/02/tools-to-generate-beautiful-api-documentation.html) 进行查看，但不推荐

## 总结

这里的内容仅作大家对这方面需求的参考，比如我最终选择了 restdown 和自建控制台，源于最快的开发速度而并不需要非常完整与强大的功能

另一点是对 HTTP OPTIONS 的扩展使用及合理的设计 RESTFul API，文档都可以省了