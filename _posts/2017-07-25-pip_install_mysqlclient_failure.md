---
layout: post
title: "Fedora 'pip install mysqlclient' failure & solution! "
date: 2017-07-25
---

When running [Flask](http://flask.pocoo.org/) and using [SQLAlchemy](https://www.sqlalchemy.org/) to provide a mechanism to update a MariaDB database through Python code I came across a problem with Fedora's implementation of MariaDB, the MySQL alternative that is packaged with Fedora. 

It was while using Flask-Migrate to update the database I came across the following error:

```
$ flask db migrate
Traceback (most recent call last):
.
.
.lots of errors
.
return __import__('MySQLdb')
ImportError: No module named MySQLdb
```

No module named MySQLdb? I tried two things, firstly installing the mysql-python client package via pip:
```
$ pip install mysqlclient
Downloading mysqlclient-1.3.10.tar.gz (82kB)
  100% |████████████████████████████████| 92kB 2.9MB/s
Building wheels for collected packages: mysqlclient
.
.
.
gcc: error: /usr/lib/rpm/redhat/redhat-hardened-cc1: No such file or directory
error: command 'gcc' failed with exit status 1
```
No luck there, nasty compile error, so I tried to install the mysql-python package via DNF

```
$ sudo dnf install mysql-python
No package mysql-python available.
Error: Unable to find a match
```

No package available. I won't go into the differences and split between MySQL and MariaDB, but this was starting to look like a compatibility issue. After lots of googling I found solutions for similar issues with Ubuntu, but nothing for Fedora. 

Then I looked at the error further, the error for `pip install mysqlclient` was ending with `gcc: error: /usr/lib/rpm/redhat/redhat-hardened-cc1: No such file or directory`. Looking into that it seemed I needed the 'redhat-rpm-config' package, so: 

`sudo dnf install redhat-rpm-config`

Once I had that installed, `pip install mysqlclient` worked a treat, and then `flask db migrate` worked as well! 



