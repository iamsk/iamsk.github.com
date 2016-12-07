---
layout: single
title: Traps in PonyORM
tags: [ponyorm, orm, python, bug]
date: 2013-05-09 13:00
---
website: http://ponyorm.com/
useage: http://doc.ponyorm.com/
tracks: http://stackoverflow.com/questions/16115713/how-pony-orm-does-its-tricks/16118756#16118756

优势及好玩的地方就不介绍了，说说可能遇到的陷阱

##more test_pony.py
    #!/usr/bin/env python
    #-*- coding: utf-8 -*-
    
    from pony.orm import Database, Required, sql_debug
    from pony.orm import select, commit
    
    db = Database('sqlite', ':memory:')


    class User(db.Entity):
        email = Required(unicode)
        password = Required(unicode)
    
    db.generate_mapping(create_tables=True)
    sql_debug(True)
    
    for i in range(2):
        user = User(email='1', password='1')
        commit()
        users = list(select(u for u in User))
        print users
        print id(users)
    
    users = list(select(u for u in User))
    print users

##python test_pony.py
    OPTIMISTIC ROLLBACK

    INSERT INTO "User" ("email", "password") VALUES (?, ?)
    [u'1', u'1']
    
    COMMIT
    
    SELECT "u"."id", "u"."email", "u"."password"
    FROM "User" "u"
    
    [User[1]]
    4453021024
    OPTIMISTIC ROLLBACK
    
    INSERT INTO "User" ("email", "password") VALUES (?, ?)
    [u'1', u'1']
    
    COMMIT
    
    [User[1]]
    4453021600
    SELECT "u"."id", "u"."email", "u"."password"
    FROM "User" "u"
    
    [User[1], User[2]]

设置为 debug 模式，可以看到 for 循环中 select 查询只有一次，这不是我们期望的

此现象也出现在单进程的 tornado server 中, handler GET 获取所有结果，POST 添加新内容，但每次得到的仍然是第一次获取的

可以改用 User.select_by_sql 这种方式

update at 23:30
提交 BUG 两小时后，作者就 fix 了
https://github.com/ponyorm/pony/commit/42ec42ab444948c407b5566752b1a51ac8c075ac
