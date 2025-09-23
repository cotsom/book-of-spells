# Kafka

### Start broker

```bash
docker run --rm -e KAFKA_BROKER_ID=2   -e KAFKA_ZOOKEEPER_CONNECT=192.168.88.253:2181 \
-e KAFKA_LISTENERS=SASL_PLAINTEXT://0.0.0.0:9092 \
-e KAFKA_ADVERTISED_LISTENERS=SASL_PLAINTEXT://192.168.88.253:9092  \
-e KAFKA_LISTENER_SECURITY_PROTOCOL_MAP=SASL_PLAINTEXT:SASL_PLAINTEXT,PLAINTEXT:PLAINTEXT \
-e KAFKA_INTER_BROKER_LISTENER_NAME=SASL_PLAINTEXT \
-e KAFKA_LOG_DIRS=/bitnami/kafka/data \
-e ALLOW_PLAINTEXT_LISTENER=yes \
-e KAFKA_CFG_SASL_ENABLED_MECHANISMS=PLAIN \
-e KAFKA_CFG_SASL_MECHANISM_INTER_BROKER_PROTOCOL=PLAIN \
-e KAFKA_OPTS="-Djava.security.auth.login.config=/opt/bitnami/kafka/config/kafka_server_jaas.conf" \
-v $PWD/kafka_server_jaas.conf:/opt/bitnami/kafka/config/kafka_server_jaas.conf \
-p 9092:9092 \
bitnami/kafka:2.8.1

#kafka_server_jaas.conf:
KafkaServer {
  org.apache.kafka.common.security.plain.PlainLoginModule required
  username="broker" password="broker-secret"
  user_broker="broker-secret"
  user_admin="admin-secret";
};
```

Write to topic

```bash
kcat -b localhost:9092 \
  -X security.protocol=SASL_PLAINTEXT \
  -X sasl.mechanisms=PLAIN \
  -X sasl.username="broker" \
  -X sasl.password="broker-secret" \
  -t lolkek -P
  
  WriteSmthText

# Ctr+D - to exit
```
