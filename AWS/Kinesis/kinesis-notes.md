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
* Fully Managed Service, no administration, automatic scaling, serverless
* NEAR REAL TIME (60 seconds latency minimum for non full batches)
* Load data into Redshift / Amazon S3, ElasticSearch / Splunk
* Supports many data formats, converstions, transformations, compression
* Pay for the amount of data going through Firehose

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

* Buffer Size (ex: 32 MB): if that buffer size is reached, it's flushed
* Buffer Time (ex: 1 minute): if that time is reached, it's flushed
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
