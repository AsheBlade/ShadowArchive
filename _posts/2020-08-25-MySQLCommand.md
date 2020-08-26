---
layout: post
title: MySQL Command
date: 2020-08-25
author: Shadow Walker
tags: [MySQL]
toc: true
---

## Overview

这是2020年1月在Banyaan课上用过的MySQL command. 直接在terminal里面跑的, 还挺常用的, 记下来. 

## Command

```SQL

Shadows-Mac-mini:~ shadowsong$ sudo mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 8
Server version: 8.0.18 MySQL Community Server - GPL







mysql> create schema test;
Query OK, 1 row affected (0.00 sec)

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| test               |
+--------------------+x
5 rows in set (0.00 sec)

mysql> use test
Database changed
mysql> show tables;
Empty set (0.00 sec)

mysql> use test;
Database changed

mysql> show tables;
Empty set (0.00 sec)

mysql> CREATE TABLE pet (name VARCHAR(20), owner MARCHER(20),
    ->        species VARCHAR(20), sex CHAR(1), birth DATE, death DATE);
Query OK, 0 rows affected (0.01 sec)

mysql> show tables;
+----------------+
| Tables_in_test |
+----------------+
| pet            |
+----------------+
1 row in set (0.00 sec)

mysql> select * from pet;
Empty set (0.01 sec)

mysql> desc pet;
+---------+-------------+------+-----+---------+-------+
| Field   | Type        | Null | Key | Default | Extra |
+---------+-------------+------+-----+---------+-------+
| name    | varchar(20) | YES  |     | NULL    |       |
| owner   | varchar(20) | YES  |     | NULL    |       |
| species | varchar(20) | YES  |     | NULL    |       |
| sex     | char(1)     | YES  |     | NULL    |       |
| birth   | date        | YES  |     | NULL    |       |
| death   | date        | YES  |     | NULL    |       |
+---------+-------------+------+-----+---------+-------+
6 rows in set (0.00 sec)

mysql> INSERT INTO pet
    ->        VALUES ('Puffball','Diane','hamster','f','1999-03-30',NULL);
Query OK, 1 row affected (0.00 sec)

mysql> desc pet;
+---------+-------------+------+-----+---------+-------+
| Field   | Type        | Null | Key | Default | Extra |
+---------+-------------+------+-----+---------+-------+
| name    | varchar(20) | YES  |     | NULL    |       |
| owner   | varchar(20) | YES  |     | NULL    |       |
| species | varchar(20) | YES  |     | NULL    |       |
| sex     | char(1)     | YES  |     | NULL    |       |
| birth   | date        | YES  |     | NULL    |       |
| death   | date        | YES  |     | NULL    |       |
+---------+-------------+------+-----+---------+-------+
6 rows in set (0.00 sec)

mysql> select * from pet;
+----------+-------+---------+------+------------+-------+
| name     | owner | species | sex  | birth      | death |
+----------+-------+---------+------+------------+-------+
| Puffball | Diane | hamster | f    | 1999-03-30 | NULL  |
+----------+-------+---------+------+------------+-------+
1 row in set (0.00 sec)

mysql> select owner from pet;
+-------+
| owner |
+-------+
| Diane |
+-------+
1 row in set (0.00 sec)

mysql> INSERT INTO pet        VALUES ('lastWhisper','DAVID','rabbit','M','1999-03-30',null);
Query OK, 1 row affected (0.00 sec)

mysql> select * from pet;
+-------------+-------+---------+------+------------+-------+
| name        | owner | species | sex  | birth      | death |
+-------------+-------+---------+------+------------+-------+
| Puffball    | Diane | hamster | f    | 1999-03-30 | NULL  |
| lastWhisper | DAVID | rabbit  | M    | 1999-03-30 | NULL  |
+-------------+-------+---------+------+------------+-------+
2 rows in set (0.00 sec)

mysql> INSERT INTO pet        VALUES ('last','Dav','cat','M','2100-03-30',null);
Query OK, 1 row affected (0.00 sec)

mysql> select * from pet;
+-------------+-------+---------+------+------------+-------+
| name        | owner | species | sex  | birth      | death |
+-------------+-------+---------+------+------------+-------+
| Puffball    | Diane | hamster | f    | 1999-03-30 | NULL  |
| lastWhisper | DAVID | rabbit  | M    | 1999-03-30 | NULL  |
| last        | Dav   | cat     | M    | 2100-03-30 | NULL  |
+-------------+-------+---------+------+------------+-------+
3 rows in set (0.00 sec)

mysql> select * from pet;
+-------------+-------+---------+------+------------+-------+
| name        | owner | species | sex  | birth      | death |
+-------------+-------+---------+------+------------+-------+
| Puffball    | Diane | hamster | f    | 1999-03-30 | NULL  |
| lastWhisper | DAVID | rabbit  | M    | 1999-03-30 | NULL  |
| last        | Dav   | cat     | M    | 2100-03-30 | NULL  |
+-------------+-------+---------+------+------------+-------+
3 rows in set (0.00 sec)

mysql> select * from pet where owner = "Diane";
+----------+-------+---------+------+------------+-------+
| name     | owner | species | sex  | birth      | death |
+----------+-------+---------+------+------------+-------+
| Puffball | Diane | hamster | f    | 1999-03-30 | NULL  |
+----------+-------+---------+------+------------+-------+
1 row in set (0.00 sec)

mysql> select from pet where owner = "Diane";
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'from pet where owner = "Diane"' at line 1
mysql> select * from pet where owner = "Diane";
+----------+-------+---------+------+------------+-------+
| name     | owner | species | sex  | birth      | death |
+----------+-------+---------+------+------------+-------+
| Puffball | Diane | hamster | f    | 1999-03-30 | NULL  |
+----------+-------+---------+------+------------+-------+
1 row in set (0.00 sec)

mysql> select * from pet where sex = "f";
+----------+-------+---------+------+------------+-------+
| name     | owner | species | sex  | birth      | death |
+----------+-------+---------+------+------------+-------+
| Puffball | Diane | hamster | f    | 1999-03-30 | NULL  |
+----------+-------+---------+------+------------+-------+
1 row in set (0.00 sec)


mysql> select owner,birth from pet where owner in ('Diane', 'DAVID');
+-------+------------+
| owner | birth      |
+-------+------------+
| Diane | 1999-03-30 |
| DAVID | 1999-03-30 |
+-------+------------+
2 rows in set (0.00 sec)



mysql> delete from pet where owner = 'Dav';
Query OK, 1 row affected (0.00 sec)

mysql> select * from pet;
+-------------+-------+---------+------+------------+-------+
| name        | owner | species | sex  | birth      | death |
+-------------+-------+---------+------+------------+-------+
| Puffball    | Diane | hamster | f    | 1999-03-30 | NULL  |
| lastWhisper | DAVID | rabbit  | M    | 1999-03-30 | NULL  |
+-------------+-------+---------+------+------------+-------+
2 rows in set (0.00 sec)

mysql> update pet set sex='f' where sex = 'M';
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0


mysql> select * from pet;
+-------------+-------+---------+------+------------+-------+
| name        | owner | species | sex  | birth      | death |
+-------------+-------+---------+------+------------+-------+
| Puffball    | Diane | hamster | f    | 1999-03-30 | NULL  |
| lastWhisper | DAVID | rabbit  | f    | 1999-03-30 | NULL  |
+-------------+-------+---------+------+------------+-------+
2 rows in set (0.00 sec)

mysql> 

```