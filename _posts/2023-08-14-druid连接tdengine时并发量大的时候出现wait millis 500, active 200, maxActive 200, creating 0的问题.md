---
layout: mypost
title: druid连接tdengine时并发量大的时候出现wait millis 500, active 200, maxActive 200, creating 0的问题
categories: [druid]
extMath: true
---

## 现象
采集设备上报的数据在服务端使用的是druid连接时序数据库进行操作存储的，隔一段时间线上日志里面就会出现<font color="red">wait millis 500, active 200, maxActive 200, creating 0</font> 的异常，每次调用完后也调用了close方法，但还是出现了连接泄漏，并且都是出现在使用多线程执行的地方，猜测可能是多线程导致的，于是查了下druid的文档，发现可以配置定期清理占用时间过长的连接。

----------
## 解决
1.   在关闭连接的地方调用dataSource.removeAbandoned(),关键代码如下,本地压测后再也没有出现这个异常问题了，不过加了这个还是存在连接泄漏的问题，但是我本地压测的时候，却没有再报<font color="red">wait millis 500, active 200, maxActive 200, creating 0</font>的错误。

```java?linenums
private void returnConnection(ResultSet resultSet,Statement statement,Connection connection){
	if(resultSet!=null){
		try {
			resultSet.close();
		} catch (SQLException e) {
			log.error("close resultSet error {}",e);
		}
	}
	if(statement!=null){
		try {
			statement.close();
		} catch (SQLException e) {
			log.error("close statement error {}",e);
		}
	}
	if(connection!=null){
		try {
			connection.close();
		} catch (SQLException e) {
			log.error("close connection error {}",e);
		} finally {
			dataSource.removeAbandoned();
		}
	}
}
```

2.  配置druid定期清理一直在占用未释放的连接，关键代码如下
~~~ java
@Bean
public DruidDataSource initConnection(){
		DruidDataSource dataSource = new DruidDataSource();
		dataSource.setDriverClassName(driverName);
		dataSource.setUrl(url);
		dataSource.setUsername(userName);
		dataSource.setPassword(password);
		dataSource.setInitialSize(initialSize);
		dataSource.setMinIdle(minIdle);
		dataSource.setMaxActive(maxActive);
		dataSource.setMaxWait(maxWait);
		dataSource.setValidationQuery(validationQuery);
		dataSource.setTimeBetweenEvictionRunsMillis(timeBetweenEvictionRunsMillis);
		dataSource.setMaxOpenPreparedStatements(maxOpenPreparedStatements);
		dataSource.setRemoveAbandoned(removeAbandoned);//是否启用连接超时回收
		dataSource.setRemoveAbandonedTimeoutMillis(removeAbandonedTimeoutMillis);//超时时间 单位毫秒
		return dataSource;
}
~~~
