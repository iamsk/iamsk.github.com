---
layout: post
title: Error when install hubot
tags: [hubot, error]
date: 2012-05-07 22:47
---

### 1. nodejs 版本问题，这个在安装 hubot 时，会提示，5-7，需重新安装

### 2. brew update 问题，这是需更新 nodejs 时，发现 brew 仓库很旧，更新时发现：

    error: The following untracked working tree files would be overwritten by merge:
    Library/Formula/cocot.rb
    Please move or remove them before you can merge.

    删除对应，并最好进入原 brew 目录进行更新；

### 3. nodejs 的更新无法覆盖相关目录，自行删除 include、share、lib等目录下 nodejs 相关文件即可
    
    brew link node
   
### 4. coffee 1.3.1 和前面版本的 parseInt 解析方式不同

in CoffeeScript version 1.2.0

    coffee> parseInt(0o0755, 8)
    Error: In repl, Parse error on line 1: Unexpected 'IDENTIFIER'
        at Object.parseError (/usr/local/lib/node_modules/coffee-script/lib/coffee-script/parser.js:470:11)
        at Object.parse (/usr/local/lib/node_modules/coffee-script/lib/coffee-script/parser.js:546:22)
        at /usr/local/lib/node_modules/coffee-script/lib/coffee-script/coffee-script.js:40:22
        at Object.eval (/usr/local/lib/node_modules/coffee-script/lib/coffee-script/coffee-script.js:123:10)
        at Interface.<anonymous> (/usr/local/lib/node_modules/coffee-script/lib/coffee-script/repl.js:51:34)
        at Interface.emit (events.js:67:17)
        at Interface._onLine (readline.js:162:10)
        at Interface._line (readline.js:426:8)
        at Interface._ttyWrite (readline.js:603:14)
        at ReadStream.<anonymous> (readline.js:82:12)
