# rabbitmq-notes

# Brokers:
Messaging brokers receive messages from publishers (applications that publish them, also known as producers) and route them to consumers (applications that process them).

The AMQP 0-9-1 Model has the following view of the world: messages are published to exchanges, which are often compared to post offices or mailboxes. Exchanges then distribute message copies to queues using rules called bindings. Then the broker either deliver messages to consumers subscribed to queues, or consumers fetch/pull messages from queues on demand.

![image](https://user-images.githubusercontent.com/30605841/109824289-aed86f80-7c06-11eb-90fc-3692c1dc4448.png)

Exchanges take a message and route it into zero or more queues. The routing algorithm used depends on the exchange type and rules called bindings. AMQP 0-9-1 brokers provide four exchange types:

## Direct exchange (Unicasting based on routing key)
   A direct exchange delivers messages to queues based on the message routing key. A direct exchange is ideal for the unicast routing of messages
   ![image](https://user-images.githubusercontent.com/30605841/109828519-b39f2280-7c0a-11eb-9228-56666111867b.png)

## Fanout exchange (Broadcasting ignoring routing key)
   A fanout exchange routes messages to all of the queues that are bound to it and the routing key is ignored. If N queues are bound to a fanout exchange, when a new message is published to that exchange a copy of the message is delivered to all N queues. Fanout exchanges are ideal for the broadcast routing of messages.
   ![image](https://user-images.githubusercontent.com/30605841/109828777-f234dd00-7c0a-11eb-862c-f6417ea78d59.png)

## Topic Exchange (Multicasting using routing key pattern)
   Topic exchanges route messages to one or many queues based on matching between a message routing key and the pattern that was used to bind a queue to an exchange. The topic exchange type is often used to implement various publish/subscribe pattern variations. Topic exchanges are commonly used for the multicast routing of messages.
   
## Queues
Queues in the AMQP 0-9-1 model are very similar to queues in other message- and task-queueing systems: they store messages that are consumed by applications. Queues share some properties with exchanges, but also have some additional properties:

Name
Durable (the queue will survive a broker restart)
Exclusive (used by only one connection and the queue will be deleted when that connection closes)
Auto-delete (queue that has had at least one consumer is deleted when last consumer unsubscribes)
Arguments (optional; used by plugins and broker-specific features such as message TTL, queue length limit, etc)

Connection: A TCP connection between your application and the RabbitMQ broker.
Channel: A virtual connection inside a connection. When publishing or consuming messages from a queue - it's all done over a channel.

Exchange: Receives messages from producers and pushes them to queues depending on rules defined by the exchange type. To receive messages, a queue needs to be bound to at least one exchange.
