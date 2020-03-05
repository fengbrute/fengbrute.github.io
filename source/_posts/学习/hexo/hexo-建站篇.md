---
title: hexo 建站篇
tags:
  - hexo
categories:
  - 学习
  - hexo
abbrlink: 96fc5219
date: 2019-08-17 21:35:34
---



##   创建`pages`

我这里同时创建了`github pages`和`coding pages` 通过`dns`设置，国内走`coding`稳定快，国外走`github`你懂的

<!-- more -->

###  GitHub Pages

登录 [GitHub](https://github.com/) 只要创建指定格式的仓库即可，格式为 `${username}.github.io`

![](https://qn.nasx.top/20190820161753.png)

`pages`设置

![](https://qn.nasx.top/20190820161834.png)

![](https://qn.nasx.top/20190820162021.png)

![](https://qn.nasx.top/20190820162108.png)

### Coding Pages

登录 [Coding](https://coding.net/) ,目前coding升级为了企业版，1-5人团队还是免费的，注册流程我就不赘述了。企业版的`pages`和个人版本的不同。迁移到了项目的`持续部署`页签下

![](https://qn.nasx.top/20190820162400.png)

## 域名dns解析添加

上述`pages`服务设置好之后，需要将自己的博客域名添加`CNAME`解析，解析路线，境外转`github`,默认`coding`

![](https://qn.nasx.top/20190820161512.png)

### hexo安装(windows)

安装需要`git`&`node`环境

### 环境安装

- [git下载安装](https://git-scm.com/download)

- [nodejs下载安装](https://nodejs.org/en/)  

### hexo安装

安装好`nodejs`后一定要换源，你懂的。

```bash
npm config set registry http://mirrors.cloud.tencent.com/npm/
```

全局安装hexo,即使换了源也要等会儿

```bash
npm install -g hexo-cli
```

### 初始化

### hexo初始化

在任意位置新建`hexo`文件夹,右键`Git Bash Here`

```bash
cd .\hexo\
hexo init
```

### 安装依赖包

刚才新建的`hexo`目录下在`Git Bash`中输入

```shell
npm install
```

## 运行hexo

还在刚才的目录，`Git Bash`中继续输入

```powershell
hexo s
```

不出意外的话，hexo应该已经启动 [点击查看是否成功](http://localhost:4000) 或者浏览器输入地址`http://localhost:4000`查看

## SSH KEYS设置

### 生成key

`Git Bash`执行

```powershell
ssh-keygen -t rsa -C "example@qq.com"
```

将个人文件夹下的`C:\Users\brute\.ssh\id_rsa.pub`的内容分别添加到`GitHub`和`Coding`

### 添加公钥

- [GitHub添加公钥](https://github.com/settings/keys)
- [Coding添加公钥](https://fart.coding.net/user/account/setting/keys)

## 修改配置文件

修改`hexo`配置文件`./_config.yml`如下

```yaml
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: 
        coding: git@e.coding.net:fart/blog.git
        github: git@github.com:fengbrute/fengbrute.github.io.git
  branch: master
```

## 部署，发布，外网访问

输入命令

```powershell
hexo d -g 
```

 [常用hexo命令](https://blog.nasx.top/posts/398458e7/)

浏览器输入自己的域名域名看看效果吧