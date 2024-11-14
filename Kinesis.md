A scalable streaming service
It is designed to ingest data from different streams
Highly available in a region by design
Streams store data for 24 hours (can store up to 326 days for extra cost)

Kinesis scales by sharding
each shard adds 1mb of ingestion and 2mb consumption

Wait, isn't this similar to [[Simple Queue Service|SQS]]?
	Sort of. Kinesis is basically a SQS beefed up
	Kinesis can have multiple consumer and is designed for huge scale ingestion.

## Kinesis Data Firehose
This is a different product than normal Kinesis

It is used to deliver high throughput to supported destinations in near real time (~60 seconds)

it support transformation of data on the fly using [[Lambda]]

Lets you deliver to...
* HTTP end points
* Splunk
* Redshift (uses S3 as an intermediate)
* ElasticSearch
* [[Simple Storage Solution|S3]]

## Kinesis Data Analytics
easy way to analyze streaming data, gain actionable insights, and respond to your business and customer needs in real time.

Provides real time processing of data using SQL

Ingests from Kinesis Data Streams or Firehose
Can access reference data from an S3 bucket (json/csv data to enrich the streaming input)
Destinations are 
* Firehose
* Lambda
* Kinesis Data Streams
Errors in processing go to in-application error stream

Use this when you need real time analytics
## Kinesis Video Streams
Makes it easy to ingest live video data from producers
	Can really be used for anything that is time-serialised

You can't access data directly via storage, only via APIs

