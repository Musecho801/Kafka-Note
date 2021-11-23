# 【Kafka入门（三）】windows安装与快速开始



## 一、安装zookeeper和kafka

安装参考：https://blog.csdn.net/weixin_38004638/article/details/91893910



#### 运行zookeeper

进入`D:\apache-zookeeper-3.6.3-bin\bin`，打开cmd输入`zkServer`



#### 运行Kafka

进入`D:\kafka_2.12-2.8.0\kafka_2.12-2.8.0`，另开一个cmd输入`.\bin\windows\kafka-server-start.bat .\config\server.properties`



## 二、快速开始

进入`D:\Kafka-2.8.0\kafka_2.13-2.8.0`，打开cmd。



### 1.创建主题

```
>.\bin\windows\kafka-topics.bat --create --topic kafka-examples --bootstrap-server localhost:9092
```

结果

```
Created topic quickstart-events.
```



### 2.查看主题

```
>.\bin\windows\kafka-topics.bat --describe --topic kafka-examples --bootstrap-server localhost:9092
```

结果

![](https://img2020.cnblogs.com/blog/1491599/202110/1491599-20211008203340353-1757099668.png)



### 3.写事件到主题中 WRITE SOME EVENTS INTO THE TOPIC

为了写（读）事件，Kafka客户端通过网络和Kafka代理交流。Kafka代理一旦收到，会以持久和容错的方式，存储这些事件。



生产者客户端 producer client

```
>.\bin\windows\kafka-console-producer.bat --topic kafka-examples --bootstrap-server localhost:9092
```

输入事件

```
>this is me.
>this is her.
>
```



Ctrl+C结束处理



### 4.读取事件 READ THE EVENTS

另开一个cmd



消费者客户端 consumer client

```
>.\bin\windows\kafka-console-consumer.bat --topic kafka-examples --from-beginning --bootstrap-server localhost:9092
```

会打印结果

```
this is me.
this is her.
```



另外，因为事件是持久的存储在Kafka中的，可以被多次消费，以及可以被多个消费者消费。

经过我的测试，开启多个消费者，都会显示存储的事件。并且开启多个生产者，也可以多方生产事件。



### 5.用Kafka Connect，导出/导入你的数据作为事件流



### 6.用Kafka Stream处理你的事件



创建maven项目，导入kafka依赖

```xml
<dependency>
	<groupId>org.apache.kafka</groupId>
	<artifactId>kafka-clients</artifactId>
	<version>2.7.0</version>
</dependency>
<dependency>
    <groupId>org.apache.kafka</groupId>
    <artifactId>kafka-streams</artifactId>
    <version>2.7.0</version>
</dependency>
```

待写
