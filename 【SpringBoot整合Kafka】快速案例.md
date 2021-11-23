# 【SpringBoot整合Kafka】快速案例

快速上手 参考：https://www.bilibili.com/video/BV1w5411b7PW?from=search&seid=5140501848119421808&spm_id_from=333.337.0.0

官网：https://docs.spring.io/spring-kafka/docs/2.5.16.RELEASE/reference/html/#introduction

官网 配置说明：https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#application-properties

<br>

<br>

1.导入依赖spring-kafka

```xml
<parent>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-parent</artifactId>
	<version>2.3.4.RELEASE</version>
</parent>

<dependencies>
	<dependency>
		<groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
	<dependency>
    	<groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
	</dependency>
</dependencies>
```

<br>

2.配置文件，配置kafka参数

```yaml
server:
  port: 8080

spring:
  kafka:
    producer:
      bootstrap-servers: 101.35.93.204:9092
    consumer:
      bootstrap-servers: ${spring.kafka.producer.bootstrap-servers}
      group-id: consumer
      enable-auto-commit: true
      auto-offset-reset: latest
```

<br>

3.写Producer

```java
@Component
public class KafkaProducer {

    @Resource
    private KafkaTemplate<String, String> kafkaTemplate;

    public void send(String topic, String message) {
        kafkaTemplate.send(topic, message);
    }
}
```

<br>

4.写Controller，使用Producer的方法

```java
package com.musecho.controller;

import com.musecho.producer.KafkaProducer;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import javax.annotation.Resource;

@RestController
public class DemoController {

    @Resource
    private KafkaProducer producer;

    @RequestMapping("/send")
    public String send(String msg) {
        System.out.println("传进controller");
        producer.send("springboot_kafka", msg);
        return "发送成功";
    }
}
```

<br>

5.写Consumer

```java
@Component
public class KafkaConsumer {

    @KafkaListener(topics = {"springboot_kafka"})
    public void consumer(String msg) {
        System.out.printf("消费者接受消息：%s", msg);
    }
}
```

<br>

6.kafka中，创建主题 springboot_kafka

<br>

7.发送请求

`http://localhost:8080/send?msg=this is the first message`

结果：

页面显示 发送成功。

控制台显示：

![](https://img2020.cnblogs.com/blog/1491599/202111/1491599-20211123193046643-922634398.png)
