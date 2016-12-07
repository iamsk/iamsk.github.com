---
layout: post
title:  Use parse for push notification
tags: push, parse
date: 2015-10-08 14:41
---
### Strategy
1. use empty string(‘’) for broadcast notification;
2. use custom key(user\_unique\_id) for direct notification.
When user first launch the app, we can bind the broadcast channel for user to get some app level notifications.
When user login the app, we can bind the custom channel based on user id to send some notifications only for this user.
When user logout the app, we need unbind the custom channel to make sure user will not get any direct notification, but also can get app level notifications.
If user uninstall the app, parse will handle this, as app level notification will not send to this mobile.
### Refs
[https://www.parse.com/docs][1]

[1]:	https://www.parse.com/docs