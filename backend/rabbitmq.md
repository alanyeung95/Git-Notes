# Introduction

## Must read
https://www.cloudamqp.com/blog/2015-05-18-part1-rabbitmq-for-beginners-what-is-rabbitmq.html

## Terms
### Advanced Message Queuing Protocol (AMQP) 
AMQP is the protocol used by RabbitMQ for messaging.

### Connection
TCP connection to the target IP address and port. The connection between your application and the RabbitMQ broker.

Reference: https://www.rabbitmq.com/connections.html#lifecycle

### Channel
A virtual connection inside a connection. When publishing or consuming messages from a queue - it's all done over a channel. 

Channels cannot exist without a connection

### EXCHANGES
Messages are not published directly to a queue; instead, the producer sends messages to an exchange. 

- Direct: 
The message is routed to the queues whose binding key exactly matches the routing key of the message. For example, if the queue is bound to the exchange with the binding key pdfprocess, a message published to the exchange with a routing key pdfprocess is routed to that queue.

- Fanout: 
A fanout exchange routes messages to all of the queues bound to it.

Fanout exchanges are ideal for the broadcast routing of messages.

- Topic: 
The topic exchange does a wildcard match between the routing key and the routing pattern specified in the binding. e.g. routing_key `a.uploaded` & `b.uploaded` -> destination `*.uploaded`

An exchange is responsible for routing the messages to different queues with the help of bindings and routing keys. A binding is a link between a queue and an exchange.

### Vhost, virtual host
Provides a way to segregate applications using the same RabbitMQ instance. 
Different users can have different permissions to different vhost and queues and exchanges can be created, so they only exist in one vhost.

# Coding

## Go example
https://www.rabbitmq.com/tutorials/tutorial-one-go.html

## Config
config can be imported or exported via json. The default name is `definitions.json`

# Others

## Compare with nats

### NATS
Pros:
1. High scalability (clustering)
2. Light-weight: It’s tiny, just a 3MB Docker image!

Cons:
1. Fire and forget, no persistence: NATS doesn’t do persistent messaging; if you’re offline, you don’t get the message.
2. No enterprise queueing


### RabbitMQ

Pros:
1. It supports a variety of message routing paradigms.
2. Flexibile Persistent solution. First, some background: both persistent and transient messages can be written to disk. Persistent messages will be written to disk as soon as they reach the queue, while transient messages will be written to disk only so that they can be evicted from memory while under memory pressure
3. Enterprise favour: nice official UI monitor

Cons:
1. Too complicated cluster/HA config and management

### Reference: 
https://www.quora.com/What-is-the-reason-that-Rabbitmq-is-more-popular-than-NATS

https://medium.com/@philipfeng/modern-open-source-messaging-apache-kafka-rabbitmq-nats-pulsar-and-nsq-ca3bf7422db5

