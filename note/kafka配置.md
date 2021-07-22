#### kafka 环境配置(默认端口9092)

+ wget https://mirrors.bfsu.edu.cn/apache/kafka/2.7.0/kafka_2.12-2.7.0.tgz
+ tar -xzf kafka_2.13-2.7.0.tgz
+ cd kafka_2.13-2.7.0
+ vi config/server.properties
  + **advertised.listeners**=PLAINTEXT://(公网ip):9092
+ bin/zookeeper-server-start.sh config/zookeeper.properties
+ bin/kafka-server-start.sh config/server.properties
+ bin/kafka-topics.sh --create --topic 'topic_name' --bootstrap-server (公网ip):9092

  

