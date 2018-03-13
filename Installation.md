# Installation Kafka

https://kafka.apache.org/quickstart

sudo apt-get install openjdk-8-jdk

cd /usr/hdp/2.6.3.0-235/kafka

## Définition de la variable d'environnement pour lancer Spark2 (+ copie du fichier dans hdfs)
```
sudo bin/zookeeper-server-start.sh config/zookeeper.properties

sudo bin/kafka-server-start.sh config/server.properties

sudo bin/kafka-topics.sh --list --zookeeper localhost:2181

sudo bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test

sudo bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --from-beginning

sudo bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic test --from-beginning --consumer.config config/consumer_1.properties

```

Il faut un fichier server.properties par broker lancé

```
sudo cp config/server.properties config/server-1.properties
sudo cp config/server.properties config/server-2.properties
```
