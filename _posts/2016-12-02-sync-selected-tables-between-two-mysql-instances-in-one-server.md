---
layout: single
title: How to sync selected tables between two mysql instances in one server
tags: [mysql, sync]
date: 2016-12-02 00:00
---
There is detail about how to set up replication in MySQL for db with two different servers: [https://www.digitalocean.com/community/tutorials/how-to-set-up-master-slave-replication-in-mysql][1], Read this article first.

For master, we only can use `binlog_do_db` with database not table, so nothing change.

For slave, we need change `binlog_do_db` with `replicate-do-table`, like `replicate-do-table = project.auth_user`, this will only sync selected table to slave db.

# Refs
* [http://dev.mysql.com/doc/refman/5.7/en/replication-options-slave.html#option\_mysqld\_replicate-do-table][2]
* [https://www.lexiconn.com/blog/2014/04/how-to-set-up-selective-master-slave-replication-in-mysql/][3]
* [https://www.percona.com/doc/percona-toolkit/2.2/pt-table-sync.html][4]

[1]:	https://www.digitalocean.com/community/tutorials/how-to-set-up-master-slave-replication-in-mysql
[2]:	http://dev.mysql.com/doc/refman/5.7/en/replication-options-slave.html#option_mysqld_replicate-do-table
[3]:	https://www.lexiconn.com/blog/2014/04/how-to-set-up-selective-master-slave-replication-in-mysql/
[4]:	https://www.percona.com/doc/percona-toolkit/2.2/pt-table-sync.html