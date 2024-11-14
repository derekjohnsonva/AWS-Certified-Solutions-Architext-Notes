---
aliases:
  - SQS
---
Public, Fully managed, highly available queues 
These queues can be Standard or FIFO
Standard allows for out of order message passing
	Much faster
	Will deliver each message at least once
FIFO is strict but slower
	Will deliver a message exactly once
	Need to have the `.fifo` suffix
Messages up to 256KB - normally messages just link to larger data

Received messages are hidden so that they are invisible to other consumer. They will reappear in the queue if they are not handled after a set amount of time (Visibility Timeout)

Dead-Letter queues can be used for problem messages

Polling types
	Short - gets the message as soon as they appear
	Long - will wait to poll if there are no messages on the queue

Encryption using [[Key Management Service|KMS]]

## Delay Queues
Allow you to postpone the delivery of messages to users
Messages will be "invisible" for a "DelaySeconds" period
	maximum "DelaySeconds" is 15 minutes

## Dead-Letter Queues
Dead letter queues allow for messages which are causing repeated processing errors to be removed
How do we identify bad messages?
	We store a ReceivedCount on each message
	We will also set a maxReceiveCount
	When the ReceivedCount is bigger than the maxReceiveCount, move to the DLQ
