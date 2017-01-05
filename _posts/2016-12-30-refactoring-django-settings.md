---
layout: single
title: 重构 django settings
tags: [django, refactoring, settings, django-configurations, 重构, 配置]
---
使用 Django 的团队，总会面临 settings.py 配置文件臃肿的问题，并且随着第三方引用涉及的配置增多及多项目存在冗余配置时，这个问题更加突出了

### 我们现有的场景

1. 多数情况下，各个项目的配置文件应该独立，但是对于一个公司内部，往往各个项目配置存在一致的情况，所以我们此处要求配置可以跨项目共用

	我们有多个项目（WEB, API, AGENCY, ERP, etc），可共用配置涉及：

	* Environment 
	* Storage (DB, Cache, etc)
	* USE\_I18N, admin theme, geoip
	* etc…

2. 单个项目有多种不同的环境（Production, Staging, Test, CI, Dev, etc）；
3. 单配置文件过于复杂，包括 Django 自带的配置，项目配置，第三方库的配置（CMS, celery, payment, swagger, ckeditor, sms, email, geoip, etc），目前已突破 1300 行。

### 基于以上问题，我认为 settings 应该被重组并至少分为以下四类

1. 公共配置
2. 项目配置
3. 第三方应用配置
4. 环境配置

### 方案一（旧方式，曾使用）

* 项目之间通过拷贝+更新的方式；
* 环境之间通过引入 local\_settings.py 这种古老的方式；

```python
try:
    from local_settings import *
except ImportError:
    pass
```

* 拆出第三方配置，改为引入，类似 local\_settings 这种；

#### 优点：
* Django 原生方式，无需大的改动，即可满足需要

#### 缺点：
* 文件级别方案无法保证更细粒度的重用，如 `INSTALLED_APPS`, `DATABASES`, etc；
* 方案不优雅，配置间依赖关系全靠导入顺序决定，不直观，新引入的配置容易破坏原配置规范；
* 配置定位不方便。

### 方案二（新方式，使用中）

django-configurations: [https://django-configurations.readthedocs.io/en/stable/][1]

1. Server specific settings: 解决环境差异；
2. Global settings defaults: 解决公用配置问题；
3. Configuration mixins: 解决第三方配置的复用。

#### 优点：
* 借助类的面向对象，可以实现各种粒度的组合与重用。

#### 缺点：
* 与 Django 原生 settings 不同，此配置基于类的形式。

[1]:	https://django-configurations.readthedocs.io/en/stable/