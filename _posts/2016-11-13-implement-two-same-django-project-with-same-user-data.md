---
layout: single
title: How to implement two same django project with same user data
tags: [django]
date: 2016-11-30 00:00
---
Assuming that we have an  e-commerce  website(ProjectA), and one shop in ProjectA is created by website owner and grow fast. So we want make this shop as an independent website(ProjectB) with a lot of custom functions but still can login with original users. Users from each websites share the same user info, username, password and profile data. 

# Scenarios
* ProjectA and ProjectB both are django project;
* They have 90% percent common in code, db schemas and logics (ProjectB is forked from ProjectA).

# Requirements

## Data
* User from ProjectA can log in ProjectB, same as opposite;
* Others should be independent in data.

## Logic
* Most logic in common but have some difference in custom.
* Use less time to implement

# Solutions
1. Two independent projects with OSS server
	Move user related data from ProjectA, Make it as a SSO server(like OpenID, CAS or OAuth), then make ProjectA and ProjectB as consumer, this may need update auth logic both for API, dashboard and Admin in ProjectA and ProjectB;
	* cleanest way
	* much time to imply this
2. Mixed in one project
	Make all ProjectB’s custom logic in ProjectA, ProjectB have the most common logic in ProjectA but need Data independent, we need split those data every where;
	 * dirty way
	* much time to imply this
3. Two independent projects with synced user data
	Sync user data from ProjectA to ProjectB with Mysql built-in support;
	* clean way
	* not much time to imply this
	* looks not good in dev groups :)
4. Looks django’s multi-db can make `Solution 3` much clean and no duplicate data, but there is a huge limitation: `no-cross-database-relations` for `InnoDB`.

# Steps (Finally choose `Solution 3`)
* Fork codebase from ProjectA;
* Update settings for ProjectB;
* Build sync User data from ProjectA to ProjectB;
* Both user meta data change like **register** and **profile update** in the same urls in ProjectA.