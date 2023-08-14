---
layout: mypost
title: druid连接tdengine时并发量大的时候出现wait millis 500, active 200, maxActive 200, creating 0的问题
categories: [druid]
extMath: true
---

## 现象
采集设备上报的数据在服务端使用的是druid连接时序数据库进行操作存储的，隔一段时间线上日志里面就会出现<font color="red">millis 500, active 200, maxActive 200, creating 0</font> 的异常，每次调用完后也调用了close方法，猜测可能出现连接泄漏了，但是代码检查了一遍，没有发现可能泄漏的地方。

----------
## 解决
在关闭连接的地方调用dataSource.removeAbandoned(),关键代码如下,本地压测后再也没有出现这个异常问题了。

```java  
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
