          
          
          ksql-datagen quickstart=pageviews format=json topic=pageviews_json maxInterval=5000
          
          
          curl -X POST -H "Content-Type: application/vnd.kafka.v2+json" -H "Accept: application/vnd.kafka.v2+json" \
              --data '{"name": "pageview_consumer", "format": "json", "auto.offset.reset": "earliest"}' \
              http://localhost:8082/consumers/pageview_consumer
              
              
              {"instance_id":"pageview_consumer","base_uri":"http://localhost:8082/consumers/pageview_consumer/instances/pageview_consumer"}%             
                                               
                                               
                                               
                                               
             
                                                                             
  curl -X POST -H "Content-Type: application/vnd.kafka.v2+json" --data '{"topics":["pageviews_json"]}' \
      http://localhost:8082/consumers/pageview_consumer/instances/pageview_consumer/subscription
      
      
 curl -X GET -H "Accept: application/vnd.kafka.json.v2+json" \
          http://localhost:8082/consumers/pageview_consumer/instances/pageview_consumer/records
          