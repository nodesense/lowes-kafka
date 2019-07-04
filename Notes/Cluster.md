
kafka-server-start $KAFKA_HOME/etc/kafka/server.properties \
  --override broker.id=1 \
  --override zookeeper.connect=k8.nodesense.ai:2181
  
  

kafka-server-start $KAFKA_HOME/etc/kafka/server.properties \
  --override broker.id=100 \
  --override log.dirs=/tmp/kafka-logs-100 \
  --override zookeeper.connect=k8.nodesense.ai:2181
  --override port=9198
  