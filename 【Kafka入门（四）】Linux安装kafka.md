# 【Kafka入门（四）】Linux安装kafka

参考视频：https://www.bilibili.com/video/BV1a4411B7V9?p=6

配置参考书籍：深入理解Kafka_核心设计与实践原理



## 一、安装kafka

### 1.整个Linux服务器

### 2.配置jdk8的环境

见 https://www.cnblogs.com/musecho/p/14564524.html



### 3.安装Zookeeper

1）官网下载`apache-zookeeper-3.6.3-bin`，并解压



2）修改配置文件`/etc/profile`

```
vi /etc/profile
```

添加内容

```
export ZOOKEEPER_HOME=/root/uninstall/apache-zookeeper-3.6.3-bin
export PATH=$PATH:$ZOOKEEPER_HOME/bin
```

执行`source/etc/profile` 使配置生效。



3）修改Zookeeper的配置文件

- 进入conf目录，将文件`zoo_sample.cfg`名称修改为`zoo.cfg`。

- 在配置文件`zoo.cfg`中修改数据目录、日志目录。

```
dataDir=/root/uninstall/apache-zookeeper-3.6.3-bin/data
dataLogDir=/root/uninstall/apache-zookeeper-3.6.3-bin/log
```

并创建这两个文件夹。

- 在`/root/uninstall/apache-zookeeper-3.6.3-bin/data/`下创建一个`myid`文件，写入一个数值，例如0。标记使用的服务器broker的编号。



4）启动即可（见下)



### 4.安装kafka

1）官网下载`kafka_2.13-3.0.0.tgz`，并解压



2）修改配置文件`/etc/profile`

```
vi /etc/profile
```

添加内容

```
export ZOOKEEPER_HOME=/root/uninstall/apache-zookeeper-3.6.3-bin
export PATH=$PATH:$ZOOKEEPER_HOME/bin
```

执行`source /etc/profile` 使配置生效。



3）修改broker的配置文件server.properties

进入`/root/uninstall/kafka_2.13-3.0.0/config`

`vi server.properties`

- 修改以下参数：

```
# broker的编号，如果集群中有多个 broker ，则每个 broker 的编号需要设置的不同
broker.id=O 
# 设置是否能删除topic
delete.topic.enable=true

# broker 监听接口
listeners=PLAINTEXT//:9092
# broker 对外提供的服务入口地址
advertised.listeners=PLAINTEXT://(你的公网ip):9092
inter.broker.listener.name=PLAINTEXT

# 存放消息日志文件的地址
log.dirs=/root/uninstall/kafka_2.13-3.0.0/kafka-logs
# Kafka 所需的 ZooKeeper 集群地址，为了方便演示，我们假设 Kafka和ZooKeeper都安装在本机
zookeeper.connect=localhost:2181/kafka
```



4）启动即可（见下）



### 5.启动Zookeeper服务

进入conf目录

```
cd /root/uninstall/apache-zookeeper-3.6.3-bin/conf
```

```
zkServer.sh start
```

以下运行成功

![](https://img2020.cnblogs.com/blog/1491599/202110/1491599-20211029180317120-1375883327.png)



**查看服务运行状态**

```
zkServer.sh status
```

![](https://img2020.cnblogs.com/blog/1491599/202110/1491599-20211029180539237-391382512.png)



*如果觉得太麻烦，可以自己写个shell脚本（我还没学）



### 5.启动Kafka服务

进入根目录

```
cd /root/uninstall/kafka_2.13-3.0.0
```

命令

```
bin/kafka-server-start.sh config/server.properties
```

![](https://img2020.cnblogs.com/blog/1491599/202111/1491599-20211101094637062-1193454793.png)



- 查看进程

  ```
  jps -l
  ```

![](https://img2020.cnblogs.com/blog/1491599/202111/1491599-20211101094917254-887249483.png)

说明kafka的进程已经成功启动
