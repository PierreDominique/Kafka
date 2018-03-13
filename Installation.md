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
```
sudo bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic test --from-beginning --consumer.config config/consumer_1.properties
```

## Création d'un nouveau broker

Il faut faire un fichier server.properties par broker lancé.
```
sudo cp config/server.properties config/server-1.properties
sudo cp config/server.properties config/server-2.properties
```
Création d'un nouveau fichier server.properties config/server-2.properties.

Il est nécessaire de modifier les informations suivantes :
 
* id broker : `broker.id=2`
* le port (à décommenter) : `listeners=PLAINTEXT://:9093` 
* chemin des logs : `log.dir=/tmp/kafka-logs-2`
* changer le localhost par l'adresse ip publique de la machine avec zookeeper : ` zookeeper.connect=localhost:2181`
