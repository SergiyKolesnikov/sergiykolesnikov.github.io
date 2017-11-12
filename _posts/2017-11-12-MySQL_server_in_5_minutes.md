---
layout: post
title: In 5 Minutes to a Remote MySQL Server
---

There are many resources on the Internet to learn SQL from scratch or to refresh your knowledge.  For example, [SQLZOO](http://sqlzoo.net) is a set of interactive lessons in which you learn SQL by writing and running SQL queries against several small databases.  But what if you want to try out your skills on your own dataset that may be larger and more complex than that on SQLZOO?  Of course you can install on your computer one of the free and open-source database systems, such as [MySQL](https://www.mysql.com/) or [PostgreSQL](https://www.postgresql.org/).  It is not difficult, but wouldn't it be nice to have a remote database set up and ready for you to experiment with, anytime and everywhere (provided an Internet access)? Read on to learn how to get it for free!

## Getting a MySQL Server

First of all you need a free account on [Pythonanywhere](https://www.pypthonanywhere.com/). After creating an account, go to the *Databases* tab in the dashboard and activate your MySQL database. You will see a page with the basic information about the database and a link that will look likes this: `<your_username>$default`.

![The Database tab and a link to the MySQL console]({{ site.baseurl }}/images/2017-11-12-MySQL_server_in_5_minutes/databases_tab.png "The Database tab and a link to the MySQL console")

Clicking on the link will get you into a [MySQL client](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) console that you can use to run SQL queries against your newly created database.  But we have to put some data into it first.

## Importing an Example Dataset

MySQL documentation site provides [a set of example datasets](https://dev.mysql.com/doc/index-other.html#rowid-3).  The World dataset, for example, contains information about countries of the world, information about some of the cities in those countries, and languages spoken in each country.  [Download the dataset](http://downloads.mysql.com/docs/world.sql.zip) and upload it to Pythonanywhere using the *Uplaod a file* button on the *Files* tab.

![Uploading a dataset]({{ site.baseurl }}/images/2017-11-12-MySQL_server_in_5_minutes/files_tab.png "Uploading a dataset")

Now switch back to the *Databases* tab and click on the link to open a MySQL console. To import the world dataset into the database run the following two commands in order:
```
system unzip world.sql.zip
source world.sql
```

Now you have the World dataset installed in your database. To see the newly created tables run
```
show tables;
```
(Note the semicolon at the end)

It should return the following output:
```
+--------------------------+
|  Tables_in_user$default  |
+--------------------------+
| city                     |
| country                  |
| countrylanguage          |
+--------------------------+
3 rows in set (0.00 sec)
```

Use the `DESCRIBE` statement to obtain information about table structure:
```
mysql> describe city;
+-------------+----------+------+-----+---------+----------------+
| Field       | Type     | Null | Key | Default | Extra          |
+-------------+----------+------+-----+---------+----------------+
| ID          | int(11)  | NO   | PRI | NULL    | auto_increment |
| Name        | char(35) | NO   |     |         |                |
| CountryCode | char(3)  | NO   | MUL |         |                |
| District    | char(20) | NO   |     |         |                |
| Population  | int(11)  | NO   |     | 0       |                |
+-------------+----------+------+-----+---------+----------------+
5 rows in set (0.00 sec)
```

That is it! You are all set and ready!

Try running a `SELECT` query:
```
mysql> select count(*) from city;
+----------+
| count(*) |
+----------+
|     4079 |
+----------+
1 row in set (0.00 sec)
```

Have fun with your remote MySQL server!

