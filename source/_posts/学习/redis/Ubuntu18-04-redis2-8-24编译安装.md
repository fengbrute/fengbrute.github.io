---
title: Ubuntu18.04 redis2.8.24编译安装
tags:
  - redis
  - Ubuntu
categories:
  - 学习
  - redis
abbrlink: 30342
date: 2019-08-22 17:34:41
---

# 平台

- `Ubuntu18.04`
- `redis-2.8.24`

<!--more-->

# 编译安装

```shell
apt install gcc make
```

进入`redis`目录执行

```shell
make
```

启动`redis-server`

```shell
redis-server &
```

