# MQ

- SQS, SNS are "cloud native" services and they're using proprietary protocols from AWS
- Traditional applications running from on-premise may use open protocols such as: MQTT, AMQP, STOMP, Openwire, WSS
- When migrating to the cloud, insteead of re-engineering the application to use SQS and SNS we can use Amazon MQ
- MQ = managed Apache ActiveMQ

- MQ doesnt scale as much as SQS/SNS
- MQ runs on a dedicated machine, can run in HA with failover
- MQ has both queue features and topic features