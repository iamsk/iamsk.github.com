---
layout: single
title:  How to implement read only and write once for s3
tags: s3
date: 2015-10-08 14:41
---

What we want is our mobile can upload files to our s3 bucket, as people can decompile the client code to get the token, we need to prevent the abuse of s3, and keep our data not tampered.

The permissions for object only have getObject and putObject, amazon treat create a new object and update a object use the same putObject action, so we can’t make them with different permissions.

Here are some other way to achieve this.

### Using Versioning
What is s3 versioning?([http://docs.aws.amazon.com/AmazonS3/latest/dev/Versioning.html][1])
We can create getObject and putObject permissions to client, but always use the version 1 for getting the right object, as other versions if there, they must created by some crackers.

### Using temp bucket only for client upload
1. create a temp bucket only for client;
2. set only putObject permission for client;
3. set lifecycle for a short time;
4. every time client create a object, we move it to production  bucket and choose another unique key for it.
5. client don’t have any permissions for this production bucket.

### Refs
[http://stackoverflow.com/questions/10592541/amazon-s3-acl-for-read-only-and-write-once-access][2]

[1]:	http://docs.aws.amazon.com/AmazonS3/latest/dev/Versioning.html
[2]:	http://stackoverflow.com/questions/10592541/amazon-s3-acl-for-read-only-and-write-once-access