An AWS implementation of Apache ActiveMQ
Both [[SNS]] and [[SQS]] are public services for topics and queues respectively
	However, many companies already have an existing topic or queue infrastructure
Amazon MQ handles this

It is an open source message broker
Support JMS API, protos such as AMQP, MQTT, OpenWire, STOMP

This is not a public service
	Does not have native AWS integration
![[Pasted image 20240929231109.png | 400]]

You should not default to using this service
