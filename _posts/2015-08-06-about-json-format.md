---
layout: post
title:  About json format
tags: [json, format]
date: 2015-08-06 18:25
---

We always want to see the json data pretty, so there are a lot of ways to achieve this.

### online web service

[json formmater and validator][1]

### chrome console

Right click and click the 'inspect element' or ALT + COMMAND + i, enter into the chrome console, write your json data and assign it to a variable, you can control it as a dict.

### terminal

read data from input:
	echo '{"test":1,"test2":2}' | python -mjson.tool

retrieve select data (In this case "test"'s value):
	echo '{"test":1,"test2":2}' | python -c 'import sys,json;data=json.loads(sys.stdin.read()); print data["test"]')

if the json data is in a file:
	python -mjson.tool filename.json

### in python code
use system command
	def print_json(data):
	        import os
	
	        cmd = "echo '%s' | python -mjson.tool" % data
	        os.system(cmd)
use json lib
	print json.dumps(json.loads(content), indent=4, ensure_ascii=False)

[1]:	http://jsonformatter.curiousconcept.com/