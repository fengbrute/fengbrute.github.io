---
title: grep
categories:
  - 学习
  - Linux
abbrlink: 56213
date: 2020-02-23 23:44:21
tags:
---

> 经常使用`grep`但都是些简单的筛选，其实还有不少参数能解决不少麻烦事情现在总结下常用的一些以作备忘。

### 比较文件不同并输出

```shell
cat a.txt
1
2
3
cat b.txt
2
grep -wvf b.txt a.txt > c.txt
cat c.txt
1
3
```

