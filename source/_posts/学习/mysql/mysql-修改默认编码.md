---
title: mysql 修改默认编码
tags:
  - mysql
categories:
  - 学习
  - mysql
abbrlink: 11140
date: 2019-08-22 18:40:42
---

# 环境

- `Ubuntu18.04`
- `mysql 5.7.27-0ubuntu0.18.04.1 (Ubuntu) `

<!--more-->

# 设置

## 修改配置

```shell
vim /etc/mysql/mysql.conf.d/mysqld.cnf
[mysqld]
...
# 在[mysqld]标签下添加编码设置
character-set-server=utf8
```

## 重启服务

```shell
service mysql restart
```

