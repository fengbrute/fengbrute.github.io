---
title: Hyper-V 安装Ubuntu18.04
tags:
  - Ubuntu
categories:
  - 学习
  - Linux
abbrlink: 44233
date: 2019-08-22 15:34:14
---

# 前言

开发经常需要`linux`环境来跑后台服务,作为`Windows10`环境下的我，对比了包括`Virtualbox`,`VMware`等多个虚拟机后果断投入了`Hyper-V`的怀抱。因为虚拟`linux` `Windows10`下最强王者一定是`Hyper-V`,原因如下

<!--more-->

- 资源利用率高
  - 首先终于可以在虚拟机的`Linux`下跑出正常`nvm`的速度了	
  - 微软自家的虚拟机，对资源的调度很棒，对比过就知道
- 方便
  - `windows10`启动后虚拟机已经启动了。
  - 关机前在`Linux`运行的服务，在开机后都还是原来的样子，不需要手动启动。

# 安装

## 开启`Hyper-V`服务

在`程序和功能`开启`Hyper-V`服务

![](https://qn.nasx.top/20190822160927.png)

然后重启电脑

## `Hyper-V`配置

### 添加外网交换机

在开始菜单找到`Hyper-V`找到`虚拟交换机管理`

![](https://qn.nasx.top/20190822161209.png)

默认交换机只能内网访问，这里我们添加可以访问外网的交换机

![](https://qn.nasx.top/20190822161434.png)

### `Ubuntu18.04`安装配置

![](https://qn.nasx.top/20190822161628.png)

![](https://qn.nasx.top/20190822162013.png)

内存这里看你电脑配置和需求了

![](https://qn.nasx.top/20190822162037.png)

选择刚才创建的交换机

![](https://qn.nasx.top/20190822162120.png)

`20g`已经够用了

![](https://qn.nasx.top/1566462219955.png)

通过官网下载好的镜像安装

![](https://qn.nasx.top/20190822162407.png)

点击`完成`

![](https://qn.nasx.top/20190822162459.png)

设置`cpu`数量

![](https://qn.nasx.top/20190822162609.png)

![](https://qn.nasx.top/20190822162706.png)

可以安装系统了

![](https://qn.nasx.top/20190822162819.png)

## `Ubuntu18.04`安装

点击启动

![](https://qn.nasx.top/20190822162949.png)

选择语言

![](https://qn.nasx.top/20190822163037.png)

回车，安装

![](https://qn.nasx.top/20190822163138.png)

选择语言，回车

![](https://qn.nasx.top/20190822163306.png)

一路回车

![](https://qn.nasx.top/20190822163358.png)

![](https://qn.nasx.top/20190822163441.png)

网卡设置这里可以默认，也可以手动设置，默认的话只要回车就好

![](https://qn.nasx.top/20190822163530.png)

手动设置的，空格键选择

![](https://qn.nasx.top/20190822163729.png)

选择手动

![](https://qn.nasx.top/20190822163755.png)

网卡手动配置

![](https://qn.nasx.top/20190822164014.png)

回车

![](https://qn.nasx.top/20190822164055.png)

换源，这里用阿里云的加速源

![](https://qn.nasx.top/20190822164233.png)

全盘安装

![](https://qn.nasx.top/20190822164327.png)

回车

![](https://qn.nasx.top/20190822164356.png)

回车

![](https://qn.nasx.top/20190822164440.png)

选择继续

![](https://qn.nasx.top/20190822164505.png)

设置账户，密码

![](https://qn.nasx.top/20190822164543.png)

空格选中开启`openssh`服务

![](https://qn.nasx.top/20190822164627.png)

`Tab`键继续安装

![](https://qn.nasx.top/20190822164720.png)

reboot

![](https://qn.nasx.top/20190822170842.png)

回车

![](https://qn.nasx.top/20190822170919.png)

至此安装完毕