---
title: 准备
abbrlink: op.wolf.error
sage: true
categories:
  - 工作
  - 指上缤纷
  - 运维
date: 2020-02-17 13:42:27
tags:
---

> 狼人杀错误日志统计，按照错误的时间先后排序，不定时更新

## 2020-02-11

### 空指针（3193个）

#### log

```shell
java.lang.NullPointerException
```

#### 解决

> 暂时容错notice为null的情况，等下次更新再看

```java
 public List<MessageMetaData> getNotice(Long roomId, String roleType)
    {
        ReplayCacheBean bean = this.replayCache.getReplay(roomId);
        List<MessageMetaData> ret = new ArrayList<>();
        if (null != bean)
        {
            List<MessageMetaData> notice = bean.getNotice();
            if (null != notice && !notice.isEmpty())
            {
                notice.forEach(v -> {
                    if (null == roleType)
                        ret.add(v);
                    else if (Arrays.asList(MessageDefinition.PUBLIC_CAN_SESS).contains(v.getType()))
                        ret.add(v);
                    else if (RoleCacheBean.TYPE_WOLF.equals(roleType) && Arrays.asList(MessageDefinition.WOLF_CAN_SEE).contains(v.getType()))
                        ret.add(v);
                    else if (RoleCacheBean.TYPE_DIVINER.equals(roleType) && Arrays.asList(MessageDefinition.DIVINER_CAN_SEE).contains(v.getType()))
                        ret.add(v);
                    else if (RoleCacheBean.TYPE_WITCH.equals(roleType) && Arrays.asList(MessageDefinition.WITCH_CAN_SEE).contains(v.getType()))
                        ret.add(v);
                    else
                    {
                    }
                });
            }
        }
        return ret;
    }
```



### 比较器提示错误（374个）

#### log

```shell
java.lang.IllegalArgumentException: Comparison method violates its general contract!
```

#### 解决

> 暂时不理，有时间了再看

### 格式化错误 （17个）

#### log

```shell
java.lang.NumberFormatException: For input string: "139 6548"
	at java.lang.NumberFormatException.forInputString(NumberFormatException.java:65)
	at java.lang.Long.parseLong(Long.java:589)
	at java.lang.Long.valueOf(Long.java:803)
	at com.h5eco.vertx.util.MethodInvokeUtils.invoke(MethodInvokeUtils.java:111)
	at com.h5eco.vertx.model.impl.CmdModelImpl.execute(CmdModelImpl.java:76)
	at com.h5eco.vertx.verticle.CommandVerticle$2$1.handle(CommandVerticle.java:81)
	at com.h5eco.vertx.verticle.CommandVerticle$2$1.handle(CommandVerticle.java:1)
	at io.vertx.core.shareddata.impl.LocalAsyncLocks$LockWaiter.lambda$acquireLock$1(LocalAsyncLocks.java:65)
	at io.vertx.core.impl.ContextImpl.executeTask(ContextImpl.java:320)
	at io.vertx.core.impl.WorkerContext.lambda$wrapTask$0(WorkerContext.java:34)
	at io.vertx.core.impl.TaskQueue.run(TaskQueue.java:76)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
	at io.netty.util.concurrent.FastThreadLocalRunnable.run(FastThreadLocalRunnable.java:30)
	at java.lang.Thread.run(Thread.java:748)
```

#### 解决

> 暂时不清楚哪里问题，先不理

### http timeout （1个）

#### log

```shell
java.net.SocketTimeoutException: Read timed out
	at java.net.SocketInputStream.socketRead0(Native Method)
	at java.net.SocketInputStream.socketRead(SocketInputStream.java:116)
	at java.net.SocketInputStream.read(SocketInputStream.java:171)
	at java.net.SocketInputStream.read(SocketInputStream.java:141)
	at sun.security.ssl.InputRecord.readFully(InputRecord.java:465)
	at sun.security.ssl.InputRecord.read(InputRecord.java:503)
	at sun.security.ssl.SSLSocketImpl.readRecord(SSLSocketImpl.java:983)
	at sun.security.ssl.SSLSocketImpl.readDataRecord(SSLSocketImpl.java:940)
	at sun.security.ssl.AppInputStream.read(AppInputStream.java:105)
	at java.io.BufferedInputStream.fill(BufferedInputStream.java:246)
	at java.io.BufferedInputStream.read(BufferedInputStream.java:265)
	at org.apache.commons.httpclient.HttpParser.readRawLine(HttpParser.java:78)
	at org.apache.commons.httpclient.HttpParser.readLine(HttpParser.java:106)
	at org.apache.commons.httpclient.HttpConnection.readLine(HttpConnection.java:1116)
	at org.apache.commons.httpclient.HttpMethodBase.readStatusLine(HttpMethodBase.java:1973)
	at org.apache.commons.httpclient.HttpMethodBase.readResponse(HttpMethodBase.java:1735)
	at org.apache.commons.httpclient.HttpMethodBase.execute(HttpMethodBase.java:1098)
	at org.apache.commons.httpclient.HttpMethodDirector.executeWithRetry(HttpMethodDirector.java:398)
	at org.apache.commons.httpclient.HttpMethodDirector.executeMethod(HttpMethodDirector.java:171)
	at org.apache.commons.httpclient.HttpClient.executeMethod(HttpClient.java:397)
	at org.apache.commons.httpclient.HttpClient.executeMethod(HttpClient.java:323)
	at com.h5eco.wolf.wechat.util.HttpConnUtils.get(HttpConnUtils.java:190)
	at com.h5eco.wolf.wechat.util.HttpConnUtils.get(HttpConnUtils.java:162)
	at com.h5eco.wolf.wechat.util.HttpConnUtils.get(HttpConnUtils.java:149)
	at com.h5eco.wolf.wechat.model.impl.WechatLoginModelImpl.getLoginUserInfo(WechatLoginModelImpl.java:92)
	at com.h5eco.wolf.wechat.model.impl.WechatLoginModelImpl.doLogin(WechatLoginModelImpl.java:53)
	at com.h5eco.vertx.model.impl.LoginModelImpl.doLogin(LoginModelImpl.java:25)
	at com.h5eco.vertx.verticle.WebsocketVerticle$1$1.handle(WebsocketVerticle.java:72)
	at com.h5eco.vertx.verticle.WebsocketVerticle$1$1.handle(WebsocketVerticle.java:1)
	at io.vertx.core.impl.ContextImpl.lambda$executeBlocking$2(ContextImpl.java:272)
	at io.vertx.core.impl.TaskQueue.run(TaskQueue.java:76)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
	at io.netty.util.concurrent.FastThreadLocalRunnable.run(FastThreadLocalRunnable.java:30)
	at java.lang.Thread.run(Thread.java:748)
```

#### 解决

> 

### 阻塞 （16个）

#### log

```shell
ertx-blocked-thread-checker|00:25:40.964|core.impl.BlockedThreadChecker|Thread Thread[vert.x-worker-thread-9,5,main] has been blocked for 61822 ms, time limit is 60000 ms
io.vertx.core.VertxException: Thread blocked
	at java.util.HashMap$TreeNode.find(HashMap.java:1878) ~[?:1.8.0_181]
	at java.util.HashMap$TreeNode.find(HashMap.java:1874) ~[?:1.8.0_181]
	at java.util.HashMap$TreeNode.find(HashMap.java:1874) ~[?:1.8.0_181]
	at java.util.HashMap$TreeNode.find(HashMap.java:1874) ~[?:1.8.0_181]
	at java.util.HashMap$TreeNode.find(HashMap.java:1874) ~[?:1.8.0_181]
	at java.util.HashMap$TreeNode.find(HashMap.java:1874) ~[?:1.8.0_181]
	at java.util.HashMap$TreeNode.getTreeNode(HashMap.java:1886) ~[?:1.8.0_181]
	at java.util.HashMap.removeNode(HashMap.java:824) ~[?:1.8.0_181]
	at java.util.HashMap.remove(HashMap.java:799) ~[?:1.8.0_181]
	at sun.security.util.MemoryCache.emptyQueue(Cache.java:299) ~[?:1.8.0_181]
	at sun.security.util.MemoryCache.put(Cache.java:361) ~[?:1.8.0_181]
	at sun.security.ssl.SSLSessionContextImpl.put(SSLSessionContextImpl.java:178) ~[?:1.8.0_181]
	at sun.security.ssl.ClientHandshaker.serverFinished(ClientHandshaker.java:1236) ~[?:1.8.0_181]
	at sun.security.ssl.ClientHandshaker.processMessage(ClientHandshaker.java:359) ~[?:1.8.0_181]
	at sun.security.ssl.Handshaker.processLoop(Handshaker.java:1052) ~[?:1.8.0_181]
	at sun.security.ssl.Handshaker.process_record(Handshaker.java:987) ~[?:1.8.0_181]
	at sun.security.ssl.SSLSocketImpl.readRecord(SSLSocketImpl.java:1072) ~[?:1.8.0_181]
	at sun.security.ssl.SSLSocketImpl.performInitialHandshake(SSLSocketImpl.java:1385) ~[?:1.8.0_181]
	at sun.security.ssl.SSLSocketImpl.writeRecord(SSLSocketImpl.java:757) ~[?:1.8.0_181]
	at sun.security.ssl.AppOutputStream.write(AppOutputStream.java:123) ~[?:1.8.0_181]
	at java.io.BufferedOutputStream.flushBuffer(BufferedOutputStream.java:82) ~[?:1.8.0_181]
	at java.io.BufferedOutputStream.flush(BufferedOutputStream.java:140) ~[?:1.8.0_181]
	at org.apache.commons.httpclient.HttpConnection.flushRequestOutputStream(HttpConnection.java:828) ~[commons-httpclient-3.1.jar:?]
	at org.apache.commons.httpclient.HttpMethodBase.writeRequest(HttpMethodBase.java:2116) ~[commons-httpclient-3.1.jar:?]
	at org.apache.commons.httpclient.HttpMethodBase.execute(HttpMethodBase.java:1096) ~[commons-httpclient-3.1.jar:?]
	at org.apache.commons.httpclient.HttpMethodDirector.executeWithRetry(HttpMethodDirector.java:398) ~[commons-httpclient-3.1.jar:?]
	at org.apache.commons.httpclient.HttpMethodDirector.executeMethod(HttpMethodDirector.java:171) ~[commons-httpclient-3.1.jar:?]
	at org.apache.commons.httpclient.HttpClient.executeMethod(HttpClient.java:397) ~[commons-httpclient-3.1.jar:?]
	at org.apache.commons.httpclient.HttpClient.executeMethod(HttpClient.java:323) ~[commons-httpclient-3.1.jar:?]
	at com.h5eco.wolf.wechat.util.HttpConnUtils.get(HttpConnUtils.java:190) ~[wolf2_game2.jar:?]
	at com.h5eco.wolf.wechat.util.HttpConnUtils.get(HttpConnUtils.java:162) ~[wolf2_game2.jar:?]
	at com.h5eco.wolf.wechat.util.HttpConnUtils.get(HttpConnUtils.java:149) ~[wolf2_game2.jar:?]
	at com.h5eco.wolf.wechat.model.impl.WechatLoginModelImpl.getLoginUserInfo(WechatLoginModelImpl.java:92) ~[wolf2_game2.jar:?]
	at com.h5eco.wolf.wechat.model.impl.WechatLoginModelImpl.doLogin(WechatLoginModelImpl.java:53) ~[wolf2_game2.jar:?]
	at com.h5eco.vertx.model.impl.LoginModelImpl.doLogin(LoginModelImpl.java:25) ~[wolf2_conn-1.6.13.jar:?]
	at com.h5eco.vertx.verticle.WebsocketVerticle$1$1.handle(WebsocketVerticle.java:72) ~[wolf2_conn-1.6.13.jar:?]
	at com.h5eco.vertx.verticle.WebsocketVerticle$1$1.handle(WebsocketVerticle.java:1) ~[wolf2_conn-1.6.13.jar:?]
	at io.vertx.core.impl.ContextImpl.lambda$executeBlocking$2(ContextImpl.java:272) ~[vertx-core-3.7.1.jar:3.7.1]
	at io.vertx.core.impl.ContextImpl$$Lambda$10/905664150.run(Unknown Source) ~[?:?]
	at io.vertx.core.impl.TaskQueue.run(TaskQueue.java:76) ~[vertx-core-3.7.1.jar:3.7.1]
	at io.vertx.core.impl.TaskQueue$$Lambda$7/898694235.run(Unknown Source) ~[?:?]
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149) ~[?:1.8.0_181]
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624) ~[?:1.8.0_181]
	at io.netty.util.concurrent.FastThreadLocalRunnable.run(FastThreadLocalRunnable.java:30) ~[netty-common-4.1.34.Final.jar:4.1.34.Final]
	at java.lang.Thread.run(Thread.java:748) ~[?:1.8.0_181]
```

#### 解决

### ssl连接异常 （1个）

#### log

```shell
javax.net.ssl.SSLHandshakeException: Remote host closed connection during handshake
	at sun.security.ssl.SSLSocketImpl.readRecord(SSLSocketImpl.java:1002)
	at sun.security.ssl.SSLSocketImpl.performInitialHandshake(SSLSocketImpl.java:1385)
	at sun.security.ssl.SSLSocketImpl.writeRecord(SSLSocketImpl.java:757)
	at sun.security.ssl.AppOutputStream.write(AppOutputStream.java:123)
	at java.io.BufferedOutputStream.flushBuffer(BufferedOutputStream.java:82)
	at java.io.BufferedOutputStream.flush(BufferedOutputStream.java:140)
	at org.apache.commons.httpclient.HttpConnection.flushRequestOutputStream(HttpConnection.java:828)
	at org.apache.commons.httpclient.HttpMethodBase.writeRequest(HttpMethodBase.java:2116)
	at org.apache.commons.httpclient.HttpMethodBase.execute(HttpMethodBase.java:1096)
	at org.apache.commons.httpclient.HttpMethodDirector.executeWithRetry(HttpMethodDirector.java:398)
	at org.apache.commons.httpclient.HttpMethodDirector.executeMethod(HttpMethodDirector.java:171)
	at org.apache.commons.httpclient.HttpClient.executeMethod(HttpClient.java:397)
	at org.apache.commons.httpclient.HttpClient.executeMethod(HttpClient.java:323)
	at com.h5eco.wolf.wechat.util.HttpConnUtils.get(HttpConnUtils.java:190)
	at com.h5eco.wolf.wechat.util.HttpConnUtils.get(HttpConnUtils.java:162)
	at com.h5eco.wolf.wechat.util.HttpConnUtils.get(HttpConnUtils.java:149)
	at com.h5eco.wolf.wechat.model.impl.WechatLoginModelImpl.getLoginUserInfo(WechatLoginModelImpl.java:92)
	at com.h5eco.wolf.wechat.model.impl.WechatLoginModelImpl.doLogin(WechatLoginModelImpl.java:53)
	at com.h5eco.vertx.model.impl.LoginModelImpl.doLogin(LoginModelImpl.java:25)
	at com.h5eco.vertx.verticle.WebsocketVerticle$1$1.handle(WebsocketVerticle.java:72)
	at com.h5eco.vertx.verticle.WebsocketVerticle$1$1.handle(WebsocketVerticle.java:1)
	at io.vertx.core.impl.ContextImpl.lambda$executeBlocking$2(ContextImpl.java:272)
	at io.vertx.core.impl.TaskQueue.run(TaskQueue.java:76)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
	at io.netty.util.concurrent.FastThreadLocalRunnable.run(FastThreadLocalRunnable.java:30)
	at java.lang.Thread.run(Thread.java:748)
Caused by: java.io.EOFException: SSL peer shut down incorrectly
	at sun.security.ssl.InputRecord.read(InputRecord.java:505)
	at sun.security.ssl.SSLSocketImpl.readRecord(SSLSocketImpl.java:983)
	... 26 more
```

#### 解决