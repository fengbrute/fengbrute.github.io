---
title: hexo next valine.min.js 加载过慢
tags:
  - hexo
categories:
  - 学习
  - hexo
abbrlink: 7c4f8010
date: 2019-08-17 23:55:59
---



## hexo配置

- hexo 3.9
- next 7.3

## 问题

晚上博客电脑登陆博客总是看不了，看了`console`是评论插件valine.min.js加载不出来，应该是cdn问题，换个cdn即可

<!-- more-->

## 解决方法

修改主题配置`hexo/themes/next/_config.yml`，`next`7.3版本配置支持换cnd源，找到`valine`源配置，然后修改为如下链接即可

```shell
  # Valine
  # Example:
  # valine: //cdn.jsdelivr.net/npm/valine@1/dist/Valine.min.js
  # valine: //cdnjs.cloudflare.com/ajax/libs/valine/1.3.4/Valine.min.js
  valine: //cdn.jsdelivr.net/npm/valine@1/dist/Valine.min.js
```

