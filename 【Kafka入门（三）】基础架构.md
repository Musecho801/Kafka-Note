# 【Kafka入门（三）】基础架构

参考：

https://www.bilibili.com/video/BV1a4411B7V9?p=5

https://my.oschina.net/jallenkwong/blog/4449224#h2_1



![](https://img2020.cnblogs.com/blog/1491599/202111/1491599-20211104151734522-689841727.png)

1.`Producer`：生产者

2.`Consumer`：消费者

3.`消费者组Consumer Group`：Consumer可以被分组到Consumer Group，提高消费能力。

topic的一个分区只能被同一个消费者组的一个消费者消费。

（Consumer A和Consumer B在同一个组，Topic A Partiton 0能被Consumer A被消费，但不能同时被Consumer B消费，可以同时被Consumer C消费；Topic A Partiton 0能被Consumer A被消费，Consumer B可以消费Topic A Partiton 1）

4.`Kafka的系统topic`：存储Consumer消费Topic的位移量（消费到哪了）。

5.`Zookeeper`：存储Kafka集群的信息。

5.`Broker`：代理。一个Kafka集群由多个broker组成。将一个broker看作一个Kafka服务实例（如果一台服务器上只部署了一个Kafka实例，则可以把一个broker看作一台Kafka服务器）。一个broker可以容纳多个topic。

6.`Topic`：主题。

7.`分区Partiton`：一个topic可以分为多个partiton，分布在多个broker上。能够提高Kafka集群的负载能力。

8.`副本Replica`：防止机器宕机，做数据冗余repilcation，同一个分区的不同副本中保存相同的消息。副本保存在不同broker上。副本之间是“一主多从“的关系。当Leader宕掉后，Follower变成Leader。

9.`Leader`：一个分区多个副本中的“主”。leader负责处理读写请求。

10.`Follower`：一个分区多个副本中的“从”。Follower只负责与leader的消息同步。

