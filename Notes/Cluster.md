
k8.nodesense.ai

zookeeper-server-start $KAFKA_HOME/etc/kafka/zookeeper.properties


kafka-server-start $KAFKA_HOME/etc/kafka/server.properties \
  --override broker.id=8 \
  --override zookeeper.connect=k8.nodesense.ai:2181
  


kafka-server-start $KAFKA_HOME/etc/kafka/server.properties \
  --override broker.id=5 \
  --override zookeeper.connect=k8.nodesense.ai:2181

kafka-server-start $KAFKA_HOME/etc/kafka/server.properties \
  --override broker.id=100 \
  --override log.dirs=/tmp/kafka-logs-100 \
  --override zookeeper.connect=k8.nodesense.ai:2181
  --override port=9198
  
  
kafka-topics --create --zookeeper k8.nodesense.ai:2181 --replication-factor 3 --partitions 3 --topic greetings

kafka-topics --describe --zookeeper k8.nodesense.ai:2181   --topic greetings

  
zookeeper-shell k8.nodesense.ai:2181

inside cli

ls /brokers/ids



kafka-topics --create --zookeeper k8.nodesense.ai:2181 --replication-factor 3 --partitions 5 --topic messages

kafka-topics --describe --zookeeper k8.nodesense.ai:2181 --topic messages
