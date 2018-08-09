# Kafka
1.Kafka相关知识 <br>
   (1)kafka使用背景 <br>
   ---是一个分布式消息系统，由LinkedIn使用Scala编写，用于LinkedIn的活动流（Activity Stream）和运营数据处理管道（Pipeline）的基础，具有高水平扩展和高吞吐量。<br>
   (2)应用领域：数据管道和消息系统的使用。<br>
   ---集成越来越多的开源分布式处理系统，例如：Apache flume（日志收集）、Apache Storm（实时数据处理）、Spark（内存处理）、elasticsearch（全局数据检索）<br>
   (3)目前用的比较多的开源分布式系统：<br>
    ![Image text](https://github.com/xx132917/kafka/blob/master/img/kfkusebg.png)<br><br>
2.kafka相关概念 <br>
   (1)AMQP协议 <br>
   ![Image text](https://github.com/xx132917/kafka/blob/master/img/amqp.png)<br><br>
   (2)Kafka支持的客户端语言:C、C++、Erlang、Java、.net、perl、PHP、Python、Ruby、Go、Javascript <br>
   (3)Kafka架构 <br>
3.zookeeper集群搭建 <br>
   (1)集群搭建 <br>
    -软件环境：
	---Linux服务器一台、三台、五台（2*n+1台,超过半数的服务器工作就能保证对外服务）<br>
	---java jdk1.7及以上 <br>
	---zookeeper 3.4.6版 <br>
   (2)集群配置参数 <br>
4.kafka集群搭建 <br>
    (1)集群搭建 <br>
    -软件环境：
	---Linux服务器一台或多台<br>
	---已经搭建好的zookeeper集群 <br>
	---kafka_2....版 <br>
	---启动kafka集群命令 <br>
   (2)集群配置参数 <br>

Linux配置Zookeeper环境搭建集群<br>
1.准备环境：<br>
（1）CentOS7 <br>
（2）三台服务器主机，IP地址：192.168.10.27、192.168.10.28、192.168.10.29  <br>

2.官网查找版本地址：<br>
![Image text](https://github.com/xx132917/kafka/blob/java/img/zk1.png)<br><br>

3.命令下载zookeeper-3.4.12.tar.gz到/opt/目录下：wget http://mirrors.shu.edu.cn/apache/zookeeper/stable/zookeeper-3.4.12.tar.gz <br>
4.解压：tar -xzvf zookeeper-3.4.12.tar.gz <br>
5.到conf目录下复制zoo_sample.cfg为zoo.cfg：cp zoo_sample.cfg zoo.cfg修改配置： <br>
![Image text](https://github.com/xx132917/kafka/blob/java/img/zk2.png)<br><br>
6.将zoo.cfg文件复制到其它服务器相同位置：<br>
(1)scp zoo.cfg  root@192.168.10.28:/opt/zookeeper-3.4.12/conf <br>
(2)scp zoo.cfg  root@192.168.10.29:/opt/zookeeper-3.4.12/conf <br>
7.在根目录的var目录下创建文件夹zookeeper，在zookeeper目录下创建文件myid，在myid文件保存服务编号： <br>
（1）mkdir /var/zookeeper <br>
（2）vim myid <br>
![Image text](https://github.com/xx132917/kafka/blob/java/img/zk3.png)<br><br>
（3）例如：编辑myid为1（server的id） <br>
8.启动三台服务器，在bin目录下：. /skServer.sh  start <br>
注：只要启动的服务器超过半数，zookeeper就能对外服务 <br>
9.使用telnet测试： <br>
（1）telnet  192.168.10.27  2181 <br>
![Image text](https://github.com/xx132917/kafka/blob/java/img/zk4.png)<br><br>
（2）继续输入state，出现如下说明集群搭建成功 <br>
![Image text](https://github.com/xx132917/kafka/blob/java/img/zk5.png)<br><br>
 
10.参考视频：http://www.jikexueyuan.com/course/1813_3.html?ss=1 <br>


Linux配置Kafka环境搭建集群 <br>
1.官网找到下载链接复制： <br>
![Image text](https://github.com/xx132917/kafka/blob/java/img/kfk1.png)<br><br>
2.下载至目录/opt/: <br>
wget http://mirrors.shu.edu.cn/apache/kafka/2.0.0/kafka_2.11-2.0.0.tgz <br>
3.解压：tar -xzvf kafka_2.11-2.0.0.tgz <br>
4.进入config文件夹配置： <br>
（1）zookeeper.properties： <br>
     ![Image text](https://github.com/xx132917/kafka/blob/java/img/kfk2.png)<br><br>
（2）sever.properties <br>
#    http://www.apache.org/licenses/LICENSE-2.0 
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# see kafka.server.KafkaConfig for additional details and defaults

############################# Server Basics #############################

# The id of the broker. This must be set to a unique integer for each broker.
broker.id=2  <br>

############################# Socket Server Settings #############################

# The address the socket server listens on. It will get the value returned from
# java.net.InetAddress.getCanonicalHostName() if not configured.
#   FORMAT:
#     listeners = listener_name://host_name:port
#   EXAMPLE:
#     listeners = PLAINTEXT://your.host.name:9092
listeners=PLAINTEXT://master:9092  <br>

# Hostname and port the broker will advertise to producers and consumers. If not set,
# it uses the value for "listeners" if configured.  Otherwise, it will use the value
# returned from java.net.InetAddress.getCanonicalHostName().
#advertised.listeners=PLAINTEXT://your.host.name:9092

# Maps listener names to security protocols, the default is for them to be the same. See the config documentation for more details
#listener.security.protocol.map=PLAINTEXT:PLAINTEXT,SSL:SSL,SASL_PLAINTEXT:SASL_PLAINTEXT,SASL_SSL:SASL_SSL

# The number of threads that the server uses for receiving requests from the network and sending responses to the network
num.network.threads=3 <br>

5.开启服务： <br>
   （1）先启动zookeeper服务 <br>
  （2）启动kafka :  bin/kafka-server-start.sh config/server.properties &（后台启动） <br>
5.创建topic：bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test <br>
  查看 topic： bin/kafka-topics.sh --list --zookeeper localhost:2181 <br>
6.模拟生产者：bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test <br>
![Image text](https://github.com/xx132917/kafka/blob/java/img/kfk3.png)<br><br>
7.  打开另一个终端模拟消费者：bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --from-beginning  <br>
![Image text](https://github.com/xx132917/kafka/blob/java/img/kfk4.png)<br><br>

Java使用kafka <br>
1.依赖Jar包： <br>
     <dependency>  <br>
       <groupId>org.apache.kafka</groupId>  <br>
       <artifactId>kafka-clients</artifactId>  <br>
       <version>2.0.0</version>  <br>
</dependency>  <br>
2.Producer API  <br>
（1）代码示例：  <br>
     Properties props = new Properties();  <br>
     //localhost为对应服务ip  <br>
     props.put("bootstrap.servers", "localhost:9092");  <br>
     props.put("acks", "all");  <br>
     props.put("retries", 0);  <br>
     props.put("batch.size", 16384);  <br>
     Props.put("linger.ms", 1);  <br>
     props.put("buffer.memory", 33554432);  <br>
     props.put("key.serializer", "org.apache.kafka.common.serialization.StringSerializer"); <br>
 props.put("value.serializer", "org.apache.kafka.common.serialization.StringSerializer");  <br>

     Producer<String, String> producer = new KafkaProducer<>(props);  <br>
     for (int i = 0; i < 100; i++)  <br>
//示例将0到99的依次放入队列  <br>
         producer.send(new ProducerRecord<String, String>("my-topic", Integer.toString(i), Integer.toString(i))); <br>
      //每次使用完，记得释放资源 <br>
      producer.close(); <br>
 
（2）参考：  <br>
http://kafka.apache.org/20/javadoc/index.html?org/apache/kafka/clients/producer/KafkaProducer.html  <br>

3.Consumer API <br>
（1）代码实例： <br>
     Properties props = new Properties();  <br>
     props.put("bootstrap.servers", "localhost:9092"); <br>
     props.put("group.id", "test");  <br>
     props.put("enable.auto.commit", "true");  <br>
     props.put("auto.commit.interval.ms", "1000");  <br>
     props.put("key.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");  <br>
     props.put("value.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");  <br>
     KafkaConsumer<String, String> consumer = new KafkaConsumer<>(props);<br>
     consumer.subscribe(Arrays.asList("test));<br>
     while (true) {  <br>
         ConsumerRecords<String, String> records = consumer.poll(100); <br>
         for (ConsumerRecord<String, String> record : records) <br>
             System.out.printf("offset = %d, key = %s, value = %s%n", record.offset(), record.key(), record.value());<br>
     }<br>
（2）参考：<br>
http://kafka.apache.org/20/javadoc/index.html?org/apache/kafka/clients/consumer/KafkaConsumer.html<br>



