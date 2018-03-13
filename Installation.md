# Installation Kafka

https://kafka.apache.org/quickstart

sudo apt-get install openjdk-8-jdk

cd /usr/hdp/2.6.3.0-235/kafka

## Exemple simple
* Démarrage du server zookeeper
```
sudo bin/zookeeper-server-start.sh config/zookeeper.properties
```

* Création d'un broker
```
sudo bin/kafka-server-start.sh config/server.properties
```

* Création d'un topic
```
sudo bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test

sudo bin/kafka-topics.sh --list --zookeeper localhost:2181 (lister les brokers)
```

* Création d'un producer
```
sudo bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test
```
* Création d'un consumer
```
sudo bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --from-beginning
```
* Création de deux consumers dans un même groupe sur deux brokers différents

```
sudo bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic test --from-beginning --consumer.config config/consumer_1.properties
sudo bin/kafka-console-consumer.sh --zookeeper 34.249.95.103:2181 --topic test --from-beginning --consumer.config config/consumer_2.properties
```

```
group.id=test-consumer-group
zookeeper.connect=127.0.0.1:2181
```

## Création d'un nouveau broker

Il faut créer un nouveau fichier server.properties par broker lancé.
```
sudo cp config/server.properties config/server-2.properties
```

Il est nécessaire de modifier les informations suivantes dans les nouveaux fichiers :
 
* id broker : `broker.id=2`
* le port (à décommenter) : `listeners=PLAINTEXT://:9093` 
* chemin des logs : `log.dir=/tmp/kafka-logs-2`
* changer le localhost par l'adresse ip publique de la machine avec zookeeper : ` zookeeper.connect=localhost:2181`


## Kill du broker 2

bin/kafka-topics.sh --describe --zookeeper localhost:2181 --topic cars-topic

Topic:cars-topic        PartitionCount:5        ReplicationFactor:3     Configs:
Topic: cars-topic       Partition: 0    Leader: 2       Replicas: 2,0,1 Isr: 2,0,1
Topic: cars-topic       Partition: 1    Leader: 3       Replicas: 3,1,2 Isr: 3,1,2
Topic: cars-topic       Partition: 2    Leader: 0       Replicas: 0,2,3 Isr: 0,2,3
Topic: cars-topic       Partition: 3    Leader: 1       Replicas: 1,3,0 Isr: 1,3,0
Topic: cars-topic       Partition: 4    Leader: 2       Replicas: 2,1,3 Isr: 2,1,3

Topic:cars-topic        PartitionCount:5        ReplicationFactor:3     Configs:
Topic: cars-topic       Partition: 0    Leader: 0       Replicas: 2,0,1 Isr: 0,1
Topic: cars-topic       Partition: 1    Leader: 3       Replicas: 3,1,2 Isr: 3,1
Topic: cars-topic       Partition: 2    Leader: 0       Replicas: 0,2,3 Isr: 0,3
Topic: cars-topic       Partition: 3    Leader: 1       Replicas: 1,3,0 Isr: 1,3,0
Topic: cars-topic       Partition: 4    Leader: 1       Replicas: 2,1,3 Isr: 1,3

Topic:cars-topic        PartitionCount:5        ReplicationFactor:3     Configs:
Topic: cars-topic       Partition: 0    Leader: 0       Replicas: 2,0,1 Isr: 0,1,2
Topic: cars-topic       Partition: 1    Leader: 3       Replicas: 3,1,2 Isr: 3,1,2
Topic: cars-topic       Partition: 2    Leader: 0       Replicas: 0,2,3 Isr: 0,3,2
Topic: cars-topic       Partition: 3    Leader: 1       Replicas: 1,3,0 Isr: 1,3,0
Topic: cars-topic       Partition: 4    Leader: 1       Replicas: 2,1,3 Isr: 1,3,2
