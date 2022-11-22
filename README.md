# Pub Sub Messaging with Kafka and Leader Election

This repo contains a `yaml` configuration file to
spin up a pub sub Kafka producer and consumer.

Additionally, it contains logic for leader election in
a case of a leader node failure.

For our setup, we have 3 Zookeepers and 3 Kafka brokers set up.

## Commands Used:

### To spin up the docker server:

```
docker-compose up -d
```

### Information about current images:

```
docker ps
```

### To start a new topic: *(Replication and partition to ensure distributed against different brokers)*

```
docker exec broker1 kafka-topics --bootstrap-server broker1:29092 --create --topic quickstart --partitions 3 --replication-factor 2
```

### To find out the current leader:

```
docker exec zookeeper1 kafka-topics --bootstrap-server broker1:29092 --topic quickstart --describe
```

### To start a producer:

```
docker exec --interactive --tty broker1 kafka-console-producer --bootstrap-server broker1:29092 --topic quickstart
```

### To start a consumer:

```
docker exec --interactive --tty broker1 kafka-console-consumer --bootstrap-server broker1:29092 --topic quickstart --from-beginning
```

### Teardown:

```
docker-compose down
```

