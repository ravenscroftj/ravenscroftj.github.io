- [RabbitMQ](https://www.rabbitmq.com/) is a FOSS message queuing system. It is a mature solution with stable clients in a number of languages
  id:: 36geytai3uekzhqgb64j3m1
## Persistence vs Durable

Durability refers to the queue metadata - if a queue is marked as durable then it will be reinitialised on restart without the client needing to set it up.

Persistence refers to the message itself. Messages with a persistent delivery-mode are written to disk as soon as they are received (and also kept in memory). Messages with a transient delivery-mode are kept in memory only. In both cases, persistent and transient messages may be dumped to disk when there is high memory pressure.
## RabbitMQ Docker Persisting Messages

When running inside Docker, rabbit uses the container id/hash as a hostname and creates a storage folder based on this e.g. `/var/lib/rabbitmq/mnesia/rabbit@824a3c6971bb/msg_stores/`. so even if we persist `/var/lib/rabbitmq/` it just generates a new subdir for whatever the container id changes to on the next run [^1]

We can set `hostname:` in docker-compose to something static to ensure that messages can be recovered.

The env var `RABBITMQ_NODENAME` refers to the bit before the @ symbol and defaults to `rabbit`.
## Client Libraries
- [[amqplib]]
## Resources

[^1]: https://stackoverflow.com/questions/41330514/docker-rabbitmq-persistency