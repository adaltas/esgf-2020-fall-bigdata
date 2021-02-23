
# Lab

## Objectives

The goal of this lab is to try Kafka consumers and producers to subscribe and publish messages, which includes the following:

1. Explore topics
2. Consume a topic
3. Produce in a topic
4. Run multiple consumers and producers

## Prerequisites

1. To execute the following code you have to be connected to the `edge-1.au.adaltas.cloud` node via SSH (and VPN).

2. We will be using the brokers’ endpoints as well as (ZooKeeper)[https://zookeeper.apache.org/], so let’s start by setting these values as [environment variables](https://en.wikipedia.org/wiki/Environment_variable).

The brokers are the list of nodes that form the Kafka cluster. In our case we have 3 nodes (`kfk-brk-1.au.adaltas.cloud`, `kfk-brk-2.au.adaltas.cloud` and `kfk-brk-3.au.adaltas.cloud`) listening on port `6667`, hence:

```bash
export brokers="kfk-brk-1.au.adaltas.cloud:6667,kfk-brk-2.au.adaltas.cloud:6667,kfk-brk-3.au.adaltas.cloud:6667"
```

The metadata of Kafka (such as topics, replication state, etc.) are stored in a ZooKeeper quorum. Interactions with topics (creation, deletion or configuration) will happen through ZooKeeper:

```bash
export zk_quorum="zoo-1.au.adaltas.cloud:2181,zoo-2.au.adaltas.cloud:2181,kfk-brk-3.au.adaltas.cloud:2181/kafka"
```

## 1. Explore topics

List all the topics in the cluster:

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh \
  --zookeeper $zk_quorum  \
  --list
```

Explore the `esgf_2020_fall_1` topic:

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh \
  --zookeeper $zk_quorum  \
  --topic esgf_2020_fall_1  \
  --describe
```

It displays an information about the topic such as:

```
Topic:esgf_2020_fall_1	PartitionCount:1	ReplicationFactor:1	Configs:
	Topic: esgf_2020_fall_1	Partition: 0	Leader: 1001	Replicas: 1001	Isr: 1001
```

## 2. Consume a topic

Run a consumer to subscribe to the `esgf_2020_fall_1` topic:

```bash
/usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh \
  --bootstrap-server $brokers \
  --consumer-property security.protocol=SASL_PLAINTEXT \
  --topic esgf_2020_fall_1 
```

Seems ok but nothing happens… It is normal, we are yet to send some data into the Kafka topic.

## 3. Produce in a topic

To do that, we will open a consumer process with the `kafka-console-producer` tool. Keep the consumer terminal tab open, and in another tab, run the following command (don’t forget about the environment variable `brokers` for the new SSH session):

```bash
/usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh \
  --broker-list $brokers \
  --producer-property security.protocol=SASL_PLAINTEXT \
  --topic esgf_2020_fall_1
```

Then, type a few messages and switch back to the previous tab (with the consumer running):

```
>This is a test
>And another one
>
```

Now, you can write your messages to CLI and all consumers will receive them. Keep this terminal window also opened.

## 4. Run multiple consumers and producers

You can connect no matter how many producers and consumers of a topic. Try to run one more producer and consumer in a separate terminal window and write messages. 

Actually, if you are not the only one who is doing this lab, you receive messages from your group mates. Let's make some fun!
