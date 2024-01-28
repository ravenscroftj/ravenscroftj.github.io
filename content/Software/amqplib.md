- AMQPLib is a [[javascript]] client for [[rabbitmq]].
## Message Persistence

To guarentee that a message will be restored if the system is reset, the queue must be durable and the message must be persistent[^1].  you can do:

```javascript
channel.assertQueue('task_queue', {durable: true});
channel.sendToQueue(queue, Buffer.from(msg), {persistent: true});
```


[^1]: https://www.rabbitmq.com/tutorials/tutorial-two-javascript.html
## Troubleshooting
### Channel closed by server: 406 (PRECONDITION-FAILED) with message "PRECONDITION\_FAILED

As explained by [this article](https://www.grzegorowski.com/rabbitmq-406-channel-closed-precondition-failed) this implies that your channel has consumed a message without ACKing or NACKing it and it has timed out. Make sure to ACK or NACK all messages when you receive them - typically after processing just in case something goes wrong there.

```typescript
this.channel?.consume(q?.queue, (msg: amqplib.ConsumeMessage | null) => {

        if(!msg){
            throw new Error(`Received a null message - weirdness.`)
        }

        try{

            const result = callback(msg)

            this.channel?.ack(msg)

            return result

        }catch(err) {
            console.log(err)
            this.channel?.nack(msg)
        }
})
```