# Kafka

  Kafka是由Apache软件基金会开发的一个开源流处理平台，由Scala和Java编写。该项目的目标是为处理实时数据提供一个统一、高吞吐、低延迟的平台。
其持久化层本质上是一个“按照分布式事务日志架构的大规模发布/订阅消息队列”，这使它作为企业级基础设施来处理流式数据非常有价值。
此外，Kafka可以通过Kafka Connect连接到外部系统（用于数据输入/输出），并提供了Kafka Streams——一个Java流式处理库 (计算机)。该设计受事务日志的影响较大。

# Kafka的架构

![Kafka的架构](https://upload.wikimedia.org/wikipedia/commons/thumb/6/64/Overview_of_Apache_Kafka.svg/800px-Overview_of_Apache_Kafka.svg.png)

Kafka存储的消息来自任意多被称为“生产者”（Producer）的进程。数据从而可以被分配到不同的“分区”（Partition）、不同的“Topic”下。在一个分区内，这些消息被索引并连同时间戳存储在一起。其它被称为“消费者”（Consumer）的进程可以从分区查询消息。Kafka运行在一个由一台或多台服务器组成的集群上，并且分区可以跨集群结点分布。

Kafka高效地处理实时流式数据，可以实现与Storm、HBase和Spark的集成。作为群集部署到多台服务器上，Kafka处理它所有的发布和订阅消息系统使用了四个API，即生产者API、消费者API、Stream API和Connector API。它能够传递大规模流式消息，自带容错功能，已经取代了一些传统消息系统，如JMS、AMQP等。

Kafka架构的主要术语包括Topic、Record和Broker。Topic由Record组成，Record持有不同的信息，而Broker则负责复制消息。Kafka有四个主要API：

- __生产者API__：支持应用程序发布Record流。
- __消费者API__：支持应用程序订阅Topic和处理Record流。
- __Stream API__：将输入流转换为输出流，并产生结果。
- __Connector API__：执行可重用的生产者和消费者API，可将Topic链接到现有应用程序

# 参考链接
[Kafka](https://kafka.apache.org/intro)
