

Broker

Producer    
    [M0, M1, M2,....]

Consumer

Topic

Partition Max 1 - Good part, consumer get same order
    P0 -  [M0, M1, M2,....]

Partition Max 2 -   consumer WILL NOT GET same order
    P0 -  [M0, M2,....]
    P1 -  [M1, M3, M5...]

    Consumer may get M3 first
    Consumer may get M0 


Consumer-Offset
_consumer_offset


Partition Max 2
    P0 -  [M0, M2]
    P1 -  [M1, M3, M5, M7, M9]

Consumer Group    props.put(GROUP_ID_CONFIG, "messages-consumer"); // offset, etc, TODO

"messages-consumer-sms-sender" - sms - 1 msg per sec
            Offset
                P0 - {
                        commited offset: 0
                    }
                P1 - 
                    {
                        commited offset: 1
                    }


"messages-consumer-email-sender" - email - 10 emails per second 
            Offset
                P0 - {
                        commited offset: 1
                    }
                P1 - 
                    {
                        commited offset: 4
                    }