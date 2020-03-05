---
title: TODO
abbrlink: 4947
sage: true
date: 2020-01-31 15:01:34
tags:
---

# TODO

| 数据总数 | 线程数 | 耗时   | redis减少 | mysql增加 |
| -------- | ------ | ------ | --------- | --------- |
| ‭306,072  | 8      | 32分钟 | 0.8G      | 0.703G    |
| ‭395,074‬  | 8      | 48分钟 | 1.19G     | 0.695G    |

| 体积  | 操作                                              | 容量减少 |
| ----- | ------------------------------------------------- | -------- |
| 8.08G | 原始                                              | 0        |
| 7.8G  | 删除top                                           | 0.28G    |
| 7.14G | 删除top&mail                                      | 0.66G    |
| 3.37G | 删除top&mail&record                               | 3.77G    |
| 2.95G | 删除top&mail&record&gift                          | 0.42G    |
| 2.07G | 删除top&mail&record&gift&tell                     | 0.88G    |
| 1.52G | 删除top&mail&record&gift&tell&friend              | 0.55G    |
| 1.48G | 删除top&mail&record&gift&tell&friend&tip          | 0.02G    |
| 1.4G  | 删除top&mail&record&gift&tell&friend&tip&mission  | 0.08G    |
| 0.8G  | 删除top&mail&record&gift&tell&friend&tip&mission& | 0.6G     |
|       |                                                   |          |
|       |                                                   |          |

| 落地前 |      |      |
| ------ | ---- | ---- |
|        |      |      |
|        |      |      |
|        |      |      |

### 新增表

1. tell
2. mail
3. friend
4. apply
5. roomuser

```shell
java.lang.IllegalArgumentException: URLDecoder: Illegal hex characters in escape (%) pattern - For input string: "平淡"
	at java.net.URLDecoder.decode(URLDecoder.java:194)
	at com.h5eco.vertx.dao.impl.SyncDaoImpl.query(SyncDaoImpl.java:157)
	at com.h5eco.clean.cache.impl.SaveCacheImpl.restore(SaveCacheImpl.java:37)
	at sun.reflect.GeneratedMethodAccessor96.invoke(Unknown Source)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.apache.commons.lang.reflect.MethodUtils.invokeMethod(MethodUtils.java:170)
	at org.apache.commons.lang.reflect.MethodUtils.invokeMethod(MethodUtils.java:131)
	at com.h5eco.vertx.model.impl.EventModelImpl.sendEvent(EventModelImpl.java:34)
	at com.h5eco.vertx.cache.impl.UserCacheImpl.get(UserCacheImpl.java:59)
	at com.h5eco.vertx.cache.impl.UserCacheImpl.backup(UserCacheImpl.java:119)
	at sun.reflect.GeneratedMethodAccessor90.invoke(Unknown Source)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.apache.commons.lang.reflect.MethodUtils.invokeMethod(MethodUtils.java:170)
	at org.apache.commons.lang.reflect.MethodUtils.invokeMethod(MethodUtils.java:131)
	at com.h5eco.vertx.model.impl.EventModelImpl.sendEvent(EventModelImpl.java:34)
	at com.h5eco.clean.thread.ThreadClean.processBackup(ThreadClean.java:169)
	at com.h5eco.clean.thread.ThreadClean.run(ThreadClean.java:137)
	at java.lang.Thread.run(Thread.java:748)
java.lang.IllegalArgumentException: URLDecoder: Illegal hex characters in escape (%) pattern - For input string: "欺人"
	at java.net.URLDecoder.decode(URLDecoder.java:194)
	at com.h5eco.vertx.dao.impl.SyncDaoImpl.query(SyncDaoImpl.java:157)
	at com.h5eco.clean.cache.impl.SaveCacheImpl.restore(SaveCacheImpl.java:37)
	at sun.reflect.GeneratedMethodAccessor96.invoke(Unknown Source)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.apache.commons.lang.reflect.MethodUtils.invokeMethod(MethodUtils.java:170)
	at org.apache.commons.lang.reflect.MethodUtils.invokeMethod(MethodUtils.java:131)
	at com.h5eco.vertx.model.impl.EventModelImpl.sendEvent(EventModelImpl.java:34)
	at com.h5eco.vertx.cache.impl.UserCacheImpl.get(UserCacheImpl.java:59)
	at com.h5eco.vertx.cache.impl.UserCacheImpl.backup(UserCacheImpl.java:119)
	at sun.reflect.GeneratedMethodAccessor90.invoke(Unknown Source)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.apache.commons.lang.reflect.MethodUtils.invokeMethod(MethodUtils.java:170)
	at org.apache.commons.lang.reflect.MethodUtils.invokeMethod(MethodUtils.java:131)
	at com.h5eco.vertx.model.impl.EventModelImpl.sendEvent(EventModelImpl.java:34)
	at com.h5eco.clean.thread.ThreadClean.processBackup(ThreadClean.java:169)
	at com.h5eco.clean.thread.ThreadClean.run(ThreadClean.java:137)
	at java.lang.Thread.run(Thread.java:748)
java.lang.IllegalArgumentException: URLDecoder: Illegal hex characters in escape (%) pattern - For input string: "[芷"
	at java.net.URLDecoder.decode(URLDecoder.java:194)
	at com.h5eco.vertx.dao.impl.SyncDaoImpl.query(SyncDaoImpl.java:157)
	at com.h5eco.clean.cache.impl.SaveCacheImpl.restore(SaveCacheImpl.java:37)
	at sun.reflect.GeneratedMethodAccessor96.invoke(Unknown Source)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.apache.commons.lang.reflect.MethodUtils.invokeMethod(MethodUtils.java:170)
	at org.apache.commons.lang.reflect.MethodUtils.invokeMethod(MethodUtils.java:131)
	at com.h5eco.vertx.model.impl.EventModelImpl.sendEvent(EventModelImpl.java:34)
	at com.h5eco.vertx.cache.impl.UserCacheImpl.get(UserCacheImpl.java:59)
	at com.h5eco.vertx.cache.impl.UserCacheImpl.backup(UserCacheImpl.java:119)
	at sun.reflect.GeneratedMethodAccessor90.invoke(Unknown Source)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.apache.commons.lang.reflect.MethodUtils.invokeMethod(MethodUtils.java:170)
	at org.apache.commons.lang.reflect.MethodUtils.invokeMethod(MethodUtils.java:131)
	at com.h5eco.vertx.model.impl.EventModelImpl.sendEvent(EventModelImpl.java:34)
	at com.h5eco.clean.thread.ThreadClean.processBackup(ThreadClean.java:169)
	at com.h5eco.clean.thread.ThreadClean.run(ThreadClean.java:137)
	at java.lang.Thread.run(Thread.java:748)

```



