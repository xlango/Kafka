# Kafka
1.Kafka相关知识 <br>
   (1)kafka使用背景 <br>
   ---是一个分布式消息系统，由LinkedIn使用Scala编写，用于LinkedIn的活动流（Activity Stream）和运营数据处理管道（Pipeline）的基础，具有高水平扩展和高吞吐量。<br>
   (2)应用领域：数据管道和消息系统的使用。<br>
   ---集成越来越多的开源分布式处理系统，例如：Apache flume（日志收集）、Apache Storm（实时数据处理）、Spark（内存处理）、elasticsearch（全局数据检索）<br>
   (3)目前用的比较多的开源分布式系统：<br>
    ![Image text](https://github.com/xx132917/Kafka/blob/master/img/kfkusebg.png)<br><br>
2.kafka相关概念 <br>
   (1)AMQP协议 <br>
   ![Image text](https://github.com/xx132917/Kafka/blob/master/img/amqp.png)<br><br>
   (2)Kafka支持的客户端语言:C、C++、Erlang、Java、.net、perl、PHP、Python、Ruby、Go、Javascript <br>
   (3)Kafka架构 <br>
3.zookeeper集群搭建 <br>
   (1)集群搭建 <br>
    -软件环境：
	---Linux服务器一台、三台、五台（2*n+1台,超过半数的服务器不能宕机）<br>
	---java jdk1.7及以上 <br>
	---zookeeper 3.4.6版 <br>
   (2)集群配置参数 <br>
4.kafka集群搭建 <br>
