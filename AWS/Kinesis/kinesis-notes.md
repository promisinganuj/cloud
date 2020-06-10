### AWS Kinesis - Highlights
* Managed "Data Streaming" service
* Great for "real-time" big data
* Great for streaming processing frameworks (Spark, NiFi etc)
* Data is automatically replicated synchronously to 3 AZs

### Three Services within AWS Kinesis
1. *Kinesis Streams:* LOW LATENCY streaming ingestion at scale
2. *Kinesis Analytics:* Perform real-time analytics on streams using SQL
3. *Kinesis FireHose:* Great for loading streams into S3, Redshift, ElasticSearch & Splunk

### Kinesis Streams
* Real-time processing with scale of throughput
* Streams are divided in ordered Shard/Partitions
* For each shard, data retention is 24 hours by default, can go up to 7 days
* Ability to repocess/replay data
* Multiple applications can consume the same stream - Not possible with Amazon SQS
* Immutablity - Once data is inserted in Kinesis, it can't be deleted - In SQS, messages can be deleted

### More about Shards
* One stream is made of many different shards
* Billing is per shard provisioned, can have as many shards as you want
* Batching available or per message calls.
* The number of shcrds can evolve over time (reshard / merge)
* Records are ordered per shard

## Kinesis Producers & Consumers
### Kinesis Producers
* AWS SDK: simple producer
* Kinesis Producer Library (KPL): batch, compression, retries, C++, Java
* Kinesis Agent: Monitor log files and sends them to kinesis directly. Can write to both Kinesis Data Streams and Kinesis Data Fireshose.

### Kinesis Consumers
* AWS SDK: simple consumer
* Lamdba (through Event source mapping)
* KCL (Kinesis Client Library): checkpointing, coordinated reads

### Kinesis Data Streams Limits
* Producer:
  * 1 MB/s or 1000 messages/s at writer PER SHARD
  * "ProvisionedThroughputException" otherwise
  
* Consumer Classic:
  * 2 MB/s at read PER SHARD across all consumers
  * 5 API calls per second PER SHARD across all consumers

* Consumer Enhanced Fan-Out:
  * 2 MB/s at read PER SHARD, PER ENHANCED CONSUMER
  * No API call needed (push mode)

* Data Retention:
  * 24 hours data retention by default
  * Can be extended to 7 days

### AWS Kinesis Data Firehose
* Amazon Kinesis Data Firehose is the easiest way to load streaming data into data stores and analytics tools.
* Load streaming data into Redshift / Amazon S3, ElasticSearch / Splunk
* Fully Managed Service, no administration, automatic scaling, serverless
* NEAR REAL TIME (60 seconds latency minimum for non full batches)
* It can batch, compress and encrypt the data before loading it.
* Pay for the amount of data going through Firehose
* Amazon Kinesis Data Firehose synchronously replicates data across three facilities in an AWS Region, providing high availability and durability for the data as it is transported to the destinations.

### Kinesis Data Firehose - Concepts
* Delivery Stream: Underlying entity of Amazon Kinesis Data Firehose. You use Firehose by creating a delivery stream and then sending data to it.

* Record: A record is the data of interest your data producer sends to a delivery stream. The maximum size of a record (before Base64-encoding) is 1024 KB.

* Destination: A destination is the data store where your data will be delivered. Amazon Kinesis Data Firehose currently supports Amazon S3, Amazon Redshift, Amazon Elasticsearch Service, and Splunk as destinations.

### Kinesis Source/Targets
* Source
  * SDK / Kinesis Producer Library (KPL)
  * Kinesis Agent
  * Kinesis Data Streams
  * CW Logs & Events
  * IoT rules actions
  
* Targets
  * Amazon S3
  * Redshift
  * ElasticSearch
  * Splunk
  * NO KCL - Different as compared to Data Streams

### Kinesis Buffer Sizing
* Firehose accumulates records in a buffer
* The buffer is flushed based on time and size rules

* Buffer Size: If that buffer size is reached, it's flushed. Buffer Size is applied before compression.
  * Range: 1MB to 128MB for S3
           1MB to 100MB for Amazon Elasticsearch Service.
 
* Buffer Time (ex: 1 minute): if that time is reached, it's flushed
  * Range: 60 Seconds to 900 seconds

* Firehose can automatically increase the buffer size to increase throughput

* High throughput => Buffer Size with be hit
* Low throughput => Buffer Time will be hit

* If real-time flush from Kinesis Data Streams to S3 is needed, use Lamdba - Much more expensive but gets the work done

### Kinesis Data Streams vs Fireshose
* Streams
 * Going to writer customer code (producer/consumer)
 * Real Time (~200 ms latency for classic, ~70 ms latency for enhachend fan-out)
 * Must manage scaling (shard splitting/merging)
 * Data Storage for 1 to 7 days, replay capability, multi consumers
 * Use with Lambda to insert data in real-tema to ElasticSearch (For Example)
 
* Fireshose
  * Fully managed, send to S3, Splunk, Redshift, ElasticSearch
  * Serverless data transformations with Lambda
  * Near real time (lowert buffer time is 1 minute)
  * Automated Scaling
  * No data storage

### Kinesis Analytics
* Kinesis Data Streams   -> Kinesis Data Analytics
* Kinesis Data Fireshose -> Kinesis Data Analytis
* Read reference tables from S3
* Create a Query in SQL
* Create output Streams and Error Streams
* Output Streams can be Kinesis Data Streams
or
* Use Kinesis Data Firehose to ingest it to S3/Redshift

### Kinesis Data Analytics - Use Cases
* Streaming ETL
* Continuous metric generation:
* Responsive analytics

### Kinesis Data Analytics - Features
* Pay only for resources consumed (not that cheap)
* Serverless: scales automatically
* Use IMA permissions to access streaming source and destination(s)
* SQL or FLink to write the computation
* Schema discovery
* Lambda can be used for pre-processing
