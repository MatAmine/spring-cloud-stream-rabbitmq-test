# spring-cloud-stream-rabbitmq-test
Test for Stream Cloud Stream with RabbitMQ (from Spring official guide)
https://dataflow.spring.io/docs/stream-developer-guides/streams/standalone-stream-rabbitmq/


Start rabbitmq on docker with the command : docker run -d -p 15672:15672 -p 5672:5672 --name rabbit-test rabbitmq:3-management
Or use a docker-file

### Start all 3 applications :
- **UsageDetailSenderRabbitApplication** : create user details and send them to a specific exchange (see application.properties for details)
- **UsageCostProcessorRabbitApplication** : receive the user details message and send user cost details on another exchange (see application.properties for details)
- **UsageCostLoggerRabbitApplication** : receive the user cost details message and log it

application.properties parameters used :

`spring.cloud.stream.bindings.output.destination=` : The output binding destination (RabbitMQ exchange) where the producer publishes the data.

`spring.cloud.stream.bindings.output.producer.requiredGroups=` : The requiredGroups to specify the consumer groups to ensure the message delivery to consumer applications.


`spring.cloud.stream.bindings.input.destination=` : the name of the exchange that the microservice is listening
`spring.cloud.stream.bindings.input.group=` : the name of the durable queue which is bound to get the message


### To check exchanges and queues through RabbitMQ management : http://localhost:15672/
