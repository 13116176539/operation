```html
# 运维笔记



## 启动kafka2.11-1.1.1.服务

 - Kafka路径

		/usr/local/kafka

 - 启动命令(后台启动)

		./bin/kafka-server-start.sh -deamon config/server.properties	
	其中1>/dev/null  2>&1 是将命令产生的输入和错误都输入到空设备，也就是不输出的意思。
	/dev/null代表空设备。
	查看是否启动有多种方式:
		netstat -tunpl | grep 9092.
		ps -ef | grep kafka
		jps
jps(Java Virtual Machine Process Status Tool)是JDK 1.5提供的一个显示当前所有java进程pid的命令，简单实用，非常适合在linux/unix平台上简单察看当前java进程的一些简单情况。
详细请看: http://swiftlet.net/archives/857

## 启动jar项目

 - jar包项目路径

		/root/cloudSystem/kafka

- 启动命令

		nohup java –Dfile.encoding=utf-8 -jar + 项目名 + &(后台启动)

## 启动zookeeper3.4.10项目

- zookeeper项目所在路径

		/usr/local/zookeeper

- 启动命令在bin目录下

		./zkServer.sh start

- 查看运行状态

		./zkServer.sh status

- 显示如下,说明启动成功.

		Mode: standalone

> **注意:**
	启动项目查看运行状态,如果报错一下信息: Error contacting service. It is probably not running.
	在/usr/local/zookeeper/data里面,删除.pid文件,重启项目即可.

## 启动dubbo2.0.6项目

- Dubbo项目所在路径

		/usr/local/tomcat8/tomcat8/webapps

- 启动命令

		./bin/startup.sh

- 关闭命令

		./bin/shutdown.sh

- 查看日志

		tail -f logs/catalina.out

## 启动mongodb3.4.7数据库

- Mongodb数据库路径

		/root/cloudSystem/mongodb-3.4.7

- 启动命令

		./bin/mongod -f conf/mongodb.conf

- 查看是否启动

		查看服务ps -ef|grep mongodb

- 查看端口号 netstat -tunpl | grep 27017

		配置mongodb开机自启动就不管了
留个坑,等会回来填

## 启动redis3.0.6数据库

- Redis安装路径

		/root/cloudSystem/redis-3.0.6

- Redis启动路径

		/usr/redis

- 启动命令

		./redis-server etc/redis.conf

- 查看是否启动

		netstat -tunpl | grep 6379
		ps -ef | grep redis

> **相关命令**
redis-server /usr..../redis.conf 启动redis服务，并指定配置文件
redis-cli 启动redis 客户端
rkill redis-server 关闭redis服务
redis-cli shutdown 关闭redis客户端
retstat -tunpl|grep 6379 查看redis 默认端口号6379占用情况

## 启动mysql5.7.25数据库

	配置了开机自启动了.不用管

​```html
<!-- English -->
<script src="../dist/js/languages/en.js"></script>

<!-- 繁體中文 -->
<script src="../dist/js/languages/zh-tw.js"></script>
​```

```