<div align="center">
    Operational bible
</div>

# 启动192.168.50.105

## 启动kafka2.11-1.1.1.服务

* Kafka路径

​       **/usr/local/kafka**

* 启动命令(****后台启动)**

​       **./bin/kafka-server-start.sh  -deamon config/server.properties          

*  查看是否启动有多种方式:**  

  **1.**     **Jps****查看**

  **jps(Java Virtual Machine Process Status Tool)****是JDK 1.5****提供的一个显示当前所有java****进程pid****的命令，简单实用，非常适合在linux/unix****平台上简单察看当前java****进程的一些简单情况。**

  详细请看: http://swiftlet.net/archives/857

  **2.**     **netstat -tunpl | grep 9092**

  **3.**     **ps -ef | grep kafka**

  

## 启动后台jar项目

* **项目路径**

  **/root/cloudSystem/kafka**

* **启动命令**

  **nohup java –Dfile.encoding=utf-8 -jar +** **项目名 + &(后台启动)**

  

## 启动zookeeper3.4.10 

* **zookeeper项目所在路径****

​       **/usr/local/zookeeper**

* **启动命令在bin目录下**

​       **./zkServer.sh start**

* **查看运行状态**

​       **./zkServer.sh status**

* **显示如下,说明启动成功.**

  **Mode: standalone**

  

## 启动dubbo2.0.6项目

* **dubbo项目所在路径**

​       **/usr/local/tomcat8/tomcat8/webapps**

* **启动命令**

​       **./bin/startup.sh**

* **关闭命令**

  **./bin/shutdown.sh**

* **查看日志**

​       **tail -f logs/catalina.out**



## 启动mongodb3.4.7数据库

* **Mongodb数据库路径**

​       **/root/cloudSystem/mongodb-3.4.7**

* **启动命令**

​       **./bin/mongod -f conf/mongodb.conf**

* **查看是否启动**

​       **查看服务ps -ef|grep mongodb**  

* **查看端口号**

  **netstat -tunpl | grep 27017 **

* **配置mongodb开机自启动**

  待完善

## 启动redis3.0.6数据库

* **Redis安装路径**

​       **/root/cloudSystem/redis-3.0.6**

* **Redis启动路径**

​       **/usr/redis**

* **启动命令**

​       **./redis-server etc/redis.conf**

* **查看是否启动**

​       **netstat -tunpl | grep 6379**   or  **ps -ef | grep redis** 

* **相关命令**

​              **redis-server /usr..../redis.conf** **启动redis**服务，并指定配置文件**

​	**redis-cli** **启动redis** **客户端**

​	**rkill redis-server** **关闭redis****服务**

​	**redis-cli shutdown** **关闭redis****客户端**

​	**retstat -tunpl|grep 6379** **查看redis** **默认端口号6379****占用情况**



## 启动mysql5.7.25数据库

配置了开机自启动了.不用管 