kafka-topics --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test

kafka-topics --list --zookeeper localhost:2181

kafka-topics --describe --zookeeper localhost:2181 --topic test


kafka-topics --alter --zookeeper localhost:2181 --topic test --partitions 

kafka-topics --alter --zookeeper localhost:2181 --topic test --partitions 9

kafka-topics --zookeeper localhost:2181 --delete --topic test

marked for deletion

kafka-server-start $KAFKA_HOME/etc/kafka/server.properties \
  --override delete.topic.enable=true \
  --override broker.id=100 \
  --override log.dirs=/tmp/kafka-logs-10 \
  --override port=9198
  
  
kafka-server-start $KAFKA_HOME/etc/kafka/server.properties \
  --override broker.id=1 \
  --override zookeeper.connect=k8.nodesense.ai:2181
  
  



 ./bin/zkCli.sh -server localhost:2181
[zk: localhost:2181(CONNECTED) 0] ls /admin/delete_topics

/bin/zkCli.sh -server localhost:2181
[zk: localhost:2181(CONNECTED) 1] ls /admin/delete_topics

 
 kafka-reassign-partitions --zookeeper localhost:2181 --reassignment-json-file replica.json --execute
 
 kafka-topics --zookeeper localhost:2181 --topic test --describe
 
 
 https://stackoverflow.com/questions/37960767/how-to-change-the-number-of-replicas-of-a-kafka-topic
 
 https://cleanprogrammer.net/how-to-increase-replication-factor-of-kafka-topic/
 