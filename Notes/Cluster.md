
kafka-server-start $KAFKA_HOME/etc/kafka/server.properties \
  --override broker.id=1 \
  --override zookeeper.connect=k8.nodesense.ai:2181
  
  
  