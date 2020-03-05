---
title: linux jdk配置
tags:
  - java
categories:
  - 学习
  - java
abbrlink: 64997
date: 2019-08-22 17:41:28
---

# 安装

## 解压官网下载的jdk压缩包

```shell
tar -zxvf jdk-8u181-linux-x64.tar.gz
mv jdk-8u181-linux-x64 jdk8
mv jdk8 /usr/local
```

<!--more-->

## 修改环境变量

```shell
# 修改环境变量
vim /etc/profile

# 添加如下代码
export CATALINA_HOME=/usr/local/tomcat
export JAVA_HOME=/usr/local/jdk8
export REDIS_HOME=/usr/local/redis-2.8.24
export PATH=".:$REDIS_HOME/src:$CATALINA_HOME/bin:$JAVA_HOME/bin:$JAVA_HOME/jre/bin:$PATH"
```

应用变量

```shell
source /etc/profile
```

