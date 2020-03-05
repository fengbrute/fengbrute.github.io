---
title: log4j2 同时控制台和写文件
abbrlink: log4j2
tags:
  - log4j
categories:
  - 学习
  - log4j
date: 2019-08-16 14:58:36
---

开发阶段有时候需要log4j2同时控制台输出以及写文件，其实，只要再logger配置多个AppenderRef就好

<!-- more -->

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE xml>
<Configuration status="INFO" monitorInterval="30">
	<Appenders>
		<RollingFile name="engine" fileName="/data/logs/wolf_table2/engine.log" filePattern="/data/logs/wolf_table2/engine_%d{yyyy-MM-dd}.log" append="true" bufferedIO="true" bufferSize="4096" ignoreExceptions="false">
			<PatternLayout pattern="%t|%d{yyyy-MM-dd HH:mm:ss,SSS}|%logger{36}|%m%n" />
			<Policies>
				<TimeBasedTriggeringPolicy interval="1" modulate="true" />
			</Policies>
		</RollingFile>

		<RollingFile name="wolf" fileName="/data/logs/wolf_table2/wolf.log" filePattern="/data/logs/wolf_table2/wolf_%d{yyyy-MM-dd}.log" append="true" bufferedIO="true" bufferSize="4096" ignoreExceptions="false">
			<PatternLayout pattern="%t|%d{yyyy-MM-dd HH:mm:ss,SSS}|%logger{36}|%m%n" />
			<Policies>
				<TimeBasedTriggeringPolicy interval="1" modulate="true" />
			</Policies>
		</RollingFile>

		<Console name="STDOUT" target="SYSTEM_OUT">
			<PatternLayout pattern="%highlight{%t|%d{HH:mm:ss.SSS}|%logger{3}|%msg%n}" />
		</Console>
	</Appenders>
	<Loggers>
		<Root level="info">
			<AppenderRef ref="STDOUT" />
		</Root>
		<Logger name="com.h5eco.engine" level="info" additivity="false">
			<AppenderRef ref="engine" />
			<AppenderRef ref="STDOUT" />
		</Logger>
		<Logger name="com.h5eco.wolf.table2" level="info" additivity="false">
			<AppenderRef ref="wolf" />
			<AppenderRef ref="STDOUT" />
		</Logger>
	</Loggers>
</Configuration>
```

