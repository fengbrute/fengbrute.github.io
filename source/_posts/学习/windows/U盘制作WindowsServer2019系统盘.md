---
title: U盘制作WindowsServer2019系统盘
tags:
  - windows
  - 系统
categories:
  - 学习
  - windows
abbrlink: 40656
date: 2019-09-08 09:40:28
---

# 问题

用`UltraISO`装`Windows Server`启动U盘，安装时提示，U盘安装Windows Server无法打开所需的文件 Sources\install.wim。

# 原因

使用UltraISO等软件刻录镜像时默认使用FAT32文件系统，该系统不支持大于4G的文件，而Windows Server的安装文件install.wim为5.12G，固安装失败。

# 解决

## 更改U盘文件系统

管理员权限运行`cmd`,并输入

```powershell
convert f: /fs:NTFS 
```

`f`改为你U盘的盘符，我这里是`f`盘

![](https://qn.nasx.top/20190908093916.png)

## 重新导入`install.wim`文件

解压`Windows Server`镜像文件，找到Sources目录下的install.wim文件，复制到对应的U盘目录下即可

