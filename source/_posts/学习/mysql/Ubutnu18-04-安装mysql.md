---
title: Ubutnu18.04 安装mysql
tags:
  - Ubuntu
  - mysql
categories:
  - 学习
  - mysql
abbrlink: 35687
date: 2019-08-22 17:56:18
---

# 环境

- `Ubuntu18.04`
- `mysql 5.7.27-0ubuntu0.18.04.1 (Ubuntu)`

# 安装

<!--more-->

## 更新源

```shell
apt update
```

## `apt`安装

```shell
apt install mysql-server
```

出现

![](https://qn.nasx.top/20190822180035.png)

输入`y`继续安装

## 配置

### 初始化配置

```shell
root@fart:/usr/local/tomcat/webapps# mysql_secure_installation

Securing the MySQL server deployment.

Connecting to MySQL using a blank password.

VALIDATE PASSWORD PLUGIN can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD plugin?

Press y|Y for Yes, any other key for No: n (我的选择)
Please set the password for root here.

New password: 

Re-enter new password: 
By default, a MySQL installation has an anonymous user,
allowing anyone to log into MySQL without having to have
a user account created for them. This is intended only for
testing, and to make the installation go a bit smoother.
You should remove them before moving into a production
environment.

Remove anonymous users? (Press y|Y for Yes, any other key for No) : y (我的选择)
Success.


Normally, root should only be allowed to connect from
'localhost'. This ensures that someone cannot guess at
the root password from the network.

Disallow root login remotely? (Press y|Y for Yes, any other key for No) : n (我的选择)

 ... skipping.
By default, MySQL comes with a database named 'test' that
anyone can access. This is also intended only for testing,
and should be removed before moving into a production
environment.


Remove test database and access to it? (Press y|Y for Yes, any other key for No) : y (我的选择)
 - Dropping test database...
Success.

 - Removing privileges on test database...
Success.

Reloading the privilege tables will ensure that all changes
made so far will take effect immediately.

Reload privilege tables now? (Press y|Y for Yes, any other key for No) : y (我的选择)
Success.

All done!
```

### 修改配置文件

```shell
vim /etc/mysql/mysql.conf.d/mysqld.cnf

#注释掉这行
#bind-address           = 127.0.0.1
```

### 赋权允许远程链接

```shell
mysql -uroot -ppasswd

use mysql;
update user set host="%" where user="root";

GRANT ALL PRIVILEGES ON *.* TO root@"%" IDENTIFIED BY "passwd";
FLUSH PRIVILEGES;
```

### 重启服务

```shell
service mysql restart
```

至此，可以内网`root`访问`mysql`了

