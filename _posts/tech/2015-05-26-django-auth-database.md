---
layout: post                                  
title: python-Flask  RESTful Authentication with Flask
category: 技术                                  
tags: [python,Flask]                                   
---

## DjangoAuth库表结构

#### 表

```
mysql> show tables;
+----------------------------+
| Tables_in_honey_manager    |
+----------------------------+
| auth_group                 |
| auth_group_permissions     |
| auth_permission            |
| auth_user                  |
| auth_user_groups           |
| auth_user_user_permissions |
| django_admin_log           |
| django_content_type        |
| django_migrations          |
| django_session             |
+----------------------------+
```

#### 表结构

1.用户档案表

```
mysql> desc auth_user;
+--------------+--------------+------+-----+---------+----------------+
| Field        | Type         | Null | Key | Default | Extra          |
+--------------+--------------+------+-----+---------+----------------+
| id           | int(11)      | NO   | PRI | NULL    | auto_increment |
| password     | varchar(128) | NO   |     | NULL    |                |
| last_login   | datetime     | YES  |     | NULL    |                |
| is_superuser | tinyint(1)   | NO   |     | NULL    |                |
| username     | varchar(30)  | NO   | UNI | NULL    |                |
| first_name   | varchar(30)  | NO   |     | NULL    |                |
| last_name    | varchar(30)  | NO   |     | NULL    |                |
| email        | varchar(254) | YES  |     | NULL    |                |
| is_staff     | tinyint(1)   | NO   |     | NULL    |                |
| is_active    | tinyint(1)   | NO   |     | NULL    |                |
| date_joined  | datetime     | NO   |     | NULL    |                |
+--------------+--------------+------+-----+---------+----------------+
```

2.小组表

```
mysql> desc auth_group;
+-------+-------------+------+-----+---------+----------------+
| Field | Type        | Null | Key | Default | Extra          |
+-------+-------------+------+-----+---------+----------------+
| id    | int(11)     | NO   | PRI | NULL    | auto_increment |
| name  | varchar(80) | NO   | UNI | NULL    |                |
+-------+-------------+------+-----+---------+----------------+
```

3.权限表

```
mysql> desc auth_permission;
+-----------------+--------------+------+-----+---------+----------------+
| Field           | Type         | Null | Key | Default | Extra          |
+-----------------+--------------+------+-----+---------+----------------+
| id              | int(11)      | NO   | PRI | NULL    | auto_increment |
| name            | varchar(255) | YES  |     | NULL    |                |
| content_type_id | int(11)      | NO   | MUL | NULL    |                |
| codename        | varchar(100) | NO   |     | NULL    |                |
+-----------------+--------------+------+-----+---------+----------------+
```

4.用户权限表

```
mysql> desc auth_user_user_permissions;
+---------------+---------+------+-----+---------+----------------+
| Field         | Type    | Null | Key | Default | Extra          |
+---------------+---------+------+-----+---------+----------------+
| id            | int(11) | NO   | PRI | NULL    | auto_increment |
| user_id       | int(11) | NO   | MUL | NULL    |                |
| permission_id | int(11) | NO   | MUL | NULL    |                |
+---------------+---------+------+-----+---------+----------------+
```

5.小组权限表

```
mysql> desc auth_group_permissions;
+---------------+---------+------+-----+---------+----------------+
| Field         | Type    | Null | Key | Default | Extra          |
+---------------+---------+------+-----+---------+----------------+
| id            | int(11) | NO   | PRI | NULL    | auto_increment |
| group_id      | int(11) | NO   | MUL | NULL    |                |
| permission_id | int(11) | NO   | MUL | NULL    |                |
+---------------+---------+------+-----+---------+----------------+
```

6.小组成员表

```
mysql> desc auth_user_groups;
+----------+---------+------+-----+---------+----------------+
| Field    | Type    | Null | Key | Default | Extra          |
+----------+---------+------+-----+---------+----------------+
| id       | int(11) | NO   | PRI | NULL    | auto_increment |
| user_id  | int(11) | NO   | MUL | NULL    |                |
| group_id | int(11) | NO   | MUL | NULL    |                |
+----------+---------+------+-----+---------+----------------+
```

操作日志记录

```
mysql> desc django_admin_log;
+-----------------+----------------------+------+-----+---------+----------------+
| Field           | Type                 | Null | Key | Default | Extra          |
+-----------------+----------------------+------+-----+---------+----------------+
| id              | int(11)              | NO   | PRI | NULL    | auto_increment |
| action_time     | datetime             | NO   |     | NULL    |                |
| object_id       | longtext             | YES  |     | NULL    |                |
| object_repr     | varchar(200)         | NO   |     | NULL    |                |
| action_flag     | smallint(5) unsigned | NO   |     | NULL    |                |
| change_message  | longtext             | NO   |     | NULL    |                |
| content_type_id | int(11)              | YES  | MUL | NULL    |                |
| user_id         | int(11)              | NO   | MUL | NULL    |                |
+-----------------+----------------------+------+-----+---------+----------------+
```

```
mysql> desc django_content_type;
+-----------+--------------+------+-----+---------+----------------+
| Field     | Type         | Null | Key | Default | Extra          |
+-----------+--------------+------+-----+---------+----------------+
| id        | int(11)      | NO   | PRI | NULL    | auto_increment |
| app_label | varchar(100) | NO   | MUL | NULL    |                |
| model     | varchar(100) | NO   |     | NULL    |                |
+-----------+--------------+------+-----+---------+----------------+
```

```
mysql> desc django_migrations;
+---------+--------------+------+-----+---------+----------------+
| Field   | Type         | Null | Key | Default | Extra          |
+---------+--------------+------+-----+---------+----------------+
| id      | int(11)      | NO   | PRI | NULL    | auto_increment |
| app     | varchar(255) | NO   |     | NULL    |                |
| name    | varchar(255) | NO   |     | NULL    |                |
| applied | datetime     | NO   |     | NULL    |                |
+---------+--------------+------+-----+---------+----------------+
```

```
mysql> desc django_session;
+--------------+-------------+------+-----+---------+-------+
| Field        | Type        | Null | Key | Default | Extra |
+--------------+-------------+------+-----+---------+-------+
| session_key  | varchar(40) | NO   | PRI | NULL    |       |
| session_data | longtext    | NO   |     | NULL    |       |
| expire_date  | datetime    | NO   | MUL | NULL    |       |
+--------------+-------------+------+-----+---------+-------+
```
