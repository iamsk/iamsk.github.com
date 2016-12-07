---
layout: single
title: How to run multiple MySQL instances in one server
tags: [mysql]
date: 2016-12-01 00:00
---
# Env
* System: Ubuntu 14.04
* Mysql-server: 5.5+

# Solutions

## Use separate `my.cnf`

### Steps
* copy the original `my.cnf` as `my2.cnf`;
* Update `pid-file`, `socket`, `port` and `datadir` in `my2.cnf`;
* Run `sudo mysql_install_db --user=mysql --datadir=/var/lib/mysql2`;
* start the second mysql server with `mysqld_safe --defaults-file=/etc/mysql/my2.cnf`, then you will have two server running.

### Pros and Cons
* Easy, use less effort to achieve;
* Not good to control, need write a new service command to handle start/stop/etc.

## Use `mysqld_multi`

### Steps
* Run `mysqld_multi --example` to show all codes we will use;
* Copy and Update `mysqld_multi` section in `my.cnf`;
* Update group name `mysqld` to `mysqld1`(make original instance controlled by `mysqld_multi`) in `my.cnf`;
* Add new group `mysqld2` in `my.cnf` with `user`, `pid-file`, `socket`, `port` and `datadir`.
* Run `sudo mysql_install_db --user=mysql --datadir=/var/lib/mysql2`;
* Use command `mysqld_multi ` to manage(start/stop ) all instances.

### Pros and Cons
* Easy, a little more than the first one;
* Easy to control, command `mysqld_multi ` build-in with mysql.

# Traps
* In MySQL 5.6, when you run `mysql_install_db`, you might get an error that says `FATAL ERROR: Could not find my-default.cnf`. Fix it by `sudo cp /etc/mysql/my.cnf /usr/share/mysql/my-default.cnf`.
* You may see `[Warning] Can't create test file /var/lib/mysql2/ip-xxx.lower-test`, this is because Ubuntu’s security check, Fix it by disable MySQL security check:
	* `sudo ln -s /etc/apparmor.d/usr.sbin.mysqld /etc/apparmor.d/disable/`
	* `sudo apparmor_parser -R /etc/apparmor.d/usr.sbin.mysqld`

# Refs
* [https://www.cyberciti.biz/faq/ubuntu-linux-howto-disable-apparmor-commands/][1]
* [https://www.percona.com/blog/2014/08/26/mysqld\_multi-how-to-run-multiple-instances-of-mysql/][2]
* [https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-14-04][3]

[1]:	https://www.cyberciti.biz/faq/ubuntu-linux-howto-disable-apparmor-commands/
[2]:	https://www.percona.com/blog/2014/08/26/mysqld_multi-how-to-run-multiple-instances-of-mysql/
[3]:	https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-14-04