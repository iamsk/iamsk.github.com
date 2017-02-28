---
layout: single
title: dev robot: hubot 
tags: [dev, auto, robot, hubot, campfire, slack]
---
[**Warning **] Please use `Slack` instead of `Hubot`!

# the structure of hubot and campfire

## campfire rooms:

+ RoomA
	+ RoomB
	+ etc...

## hubots

+ HubotA
	+ HubotB
	+ etc…

## People

+ PeopleA
	+ PeopleB
	+ etc...

the process of one command:

PeopleN send one command in RoomN, HubotN receive this command, execute and return info.

When one hubot starts, they will monitoring all executable tasks under his folder;

Rooms is based on HUBOT\_CAMPFIRE\_ACCOUNT, HUBOT\_CAMPFIRE\_TOKEN and HUBOT\_CAMPFIRE\_ROOMS

there are two methods for each hubot: respond and hear

* respond: receive all requests from exactly hubotN;
* hear: receive all requests from related rooms.

Pros for only one hubot:

1. Easy to manage;
2. Only need one repo.

Cons for only one hubot:

1. Each script have different running env, such as Intranet, Network or VPN, one hubot only can stay in one env;
2. Some thing like github campfire hook which send cmds without hubot name, then we must use hear or create new hubot and name with the first word.

With fine-grained privileges required, we can make each people as unit.

hubot can’t send commands to himself as they use the same campfire token.
