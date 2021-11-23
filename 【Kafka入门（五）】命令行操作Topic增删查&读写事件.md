# 【Kafka入门（五）】命令行操作Topic增删查&读写事件

进入kafka的根目录

- 创建主题

  --create

  ```
  bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --topic quickstart-events --replication-factor 1 --partitions 1
  ```

  ![](https://img2020.cnblogs.com/blog/1491599/202111/1491599-20211103164529635-2031434456.png)

  - `--replication-factor`：复制因子
  - `--partitions`：分区数

  在kafka-logs中，可以看到新建的主题，0是分区号

  ![](https://img2020.cnblogs.com/blog/1491599/202111/1491599-20211112182124125-629449101.png)

- 查看指定主题

  --describe

  ```
  bin/kafka-topics.sh --describe --bootstrap-server localhost:9092 --topic quickstart-events 
  ```

  ![](https://img2020.cnblogs.com/blog/1491599/202111/1491599-20211103164749856-1241138649.png)

- 查看当前服务器中的所有主题

  --list

  ```
  bin/kafka-topics.sh --list --bootstrap-server localhost:9092
  ```

  ![](https://img2020.cnblogs.com/blog/1491599/202111/1491599-20211112181344744-438080035.png)

- 删除主题

  --delete

  ```
  bin/kafka-topics.sh --delete --bootstrap-server localhost:9092 --topic kafka-examples-output
  ```

  

- 生产者 写事件

  ```
  bin/kafka-console-producer.sh --topic quickstart-events --bootstrap-server localhost:9092
  ```

- 消费者 读事件

  ```
  bin/kafka-console-consumer.sh --topic quickstart-events --from-beginning --bootstrap-server localhost:9092
  ```



