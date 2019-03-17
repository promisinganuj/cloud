## GCP Storage Options:
### Cloud Storage
- Object storage, not FILE or BLOCK Storage
- Arbitrary bunch of bites addressed via Unique Key
- This unique key is often a URL
- No need to provision ahead of time
- You would not use Cloud Storage as the root file system of your Linux box instead Cloud Storage is comprised of buckets you create and configure and use to hold your storage objects.
- Storage objects are immutable, new versions can be created if versioning is enabled.
- Data at rest is by default encrypted, data-in-transit is encrypted using HTTPS.
- Objects are organized in buckets. Each bucket has a globally unique name.
- Also, the geographic location is specified for each bucket.
- Also, assign it a default storage class.
- In addition to Cloud IAM, Access Control Lists (ACLs) can be used for finer control. Each ACL has two key pieces of information:
1. **Scope**: Who can perform the specific action
2. **Permission**: what actions can be performed
-   Cloud Storage also offers lifecycle management policies:
1. Delete object older than 365 days
2. Delete objects created before 01-Mar-2017
3. Keep only the latest 3 versions etc.
- Four Different Storage Classes:
o   Multi-regional (High Performing, 99.95% Availability SLA)

o   Regional (High Performing, 99.90% Availability SLA)

o   Nearline (Backup and Archival storage, 99.00% Availability SLA, Additional Retrieval fee)

o   Coldline (Backup and Archival storage, 99.00% Availability SLA, Additional Retrieval fee)

-   Bringing data in Cloud Storage:

o   Using “GSUtil”: Cloud storage command from cloud SDK

o   Drag-n-Drop using Chrome

o   Online Storage transfer service

o   Offline transfer appliance

o   Import/Export tables to/from BigQuery as well as Cloud SQL

 

Cloud Bigtable:

-   Google’s NoSQL big database service

-   Databases in bigtable are sparsely populated tables that can scale to billions of rows and thousands of columns and can store petabytes of data

-   High throughput, both read and write

-   The applications between HBase and Bigtable are portable; Cloud bigtable is offered through the same open source API as HBase.

-   All data in Cloud Bigtable is encrypted in both in-flight and at rest.

-   DOESN’T support SQL queries

-   DOESN’T support multi-row transactions

-   Reading/Writing Bigtable

o   Applications can interact through a data service layer like Managed VMs, the HBase rest server or a Java Server using the HBase client.

o   Data can also be streamed via Cloud Dataflow streaming, Spark Streaming and Storm

o   Through batch processes like Hadoop Map-reduce, Dataflow or Spark

 

Cloud SQL:

-   Google’s relational database service

-   2 choices: MySQL or PostgreSQL database engines as fully managed service

 

Cloud Spanner:

-   Offers transactional consistency at a global scale, schemas, SQL, and automatic synchronous replication for high availability.

-   Consider using Cloud Spanner if:

o   you have outgrown any relational database

o   sharding your databases for throughput high performance

o   need transactional consistency, global data and strong consistency

o   Database Consolidation

 

Cloud DataStore:

-   Highly scalable noSQL database

-   Also, suitable for unstructured data

-   Main usecase is to store structured data from App Engine apps.

-   Also, as an integration point between App Engine and Compute Engine

-   It offers transactions that affect multiple database rows

-   Allows SQL-like queries

-   Free daily Quota

 

Comparison:

cid:image001.png@01D4DB27.696A03F0

 

Q&A:

1. You are developing an application that transcodes large video files. Which storage option is the best choice for your application?

   Cloud Storage: Blobstore

 

2. You manufacture devices with sensors and need to stream huge amounts of data from these devices to a storage option in the cloud. Which Google Cloud Platform storage option is the best choice for your application?

   Cloud Bigtable: Ideal for data streaming because of high throughput

 

3. Which statement is true about objects in Cloud Storage?

   They are immutable, and new versions overwrite old unless you turn on versioning.

 

4. You are building a small application. If possible, you'd like this application's data storage to be at no additional charge. Which service has a free daily quota, separate from any free trials?

   Cloud Datastore: Comes with free daily quota

 

5. How do the Nearline and Coldline storage classes differ from Multi-regional and Regional? Choose all that are correct (2 responses).

   Nearline and Coldline assess additional retrieval fees.

   Nearline and Coldline use a differently-architected API.

 

6. Your application needs a relational database, and it expects to talk to MySQL. Which storage option is the best choice for your application?

   Cloud SQL

 

7. Your application needs to store data with strong transactional consistency, and you want seamless scaling up. Which storage option is the best choice for your application?

   Cloud Spanner: transactional consistency at global scale

 

8. Which GCP storage service is often the ingestion point for data being moved into the cloud, and is frequently the long-term storage location for data?

   Cloud Storage

 

9. Your Cloud Storage objects live in buckets. Which of these characteristics do you define on a per-bucket basis? Choose all that are correct:

  A geographic location

   A default storage class

   A globally-unique name

 

10. True or false: Cloud Storage is well suited to providing the root file system of a Linux virtual machine.

    FALSE: That's correct! Cloud Storage is object storage rather than file storage. Compute Engine virtual machines use Persistent Disk storage to contain their file systems.

 

11. Why would a customer consider the Coldline storage class?

    To save money on storing infrequently accessed data. Data stored in Coldline is billed at a low monthly storage rate, although a fee is assessed on retrievals.

 

12. True or false: Each table in NoSQL databases such as Cloud Bigtable has a single schema that is enforced by the database engine itself.

    FALSE. NoSQL databases such as Cloud Bigtable are suitable when all items in the database needn't have their integrity checked by a database schema. Why not? Maybe you want your database items to contain variable fields, or maybe because you simply want your application to manage database integrity.

 

13. Some developers think of Cloud Bigtable as a persistent hashtable. What does that mean?

    Each item in the database can be sparsely populated, and is looked up with a single key.

 

14. Which database service can scale to higher database sizes?

    Cloud Spanner. Cloud Spanner can scale to petabyte database sizes, while Cloud SQL is limited by the size of the database instances you choose. At the time this quiz was created, the maximum was 10,230 GB.

 

15. Which database service presents a MySQL or PostgreSQL interface to clients?

    Cloud SQL. Each Cloud SQL database is configured at creation time for either MySQL or PostgreSQL. Cloud Spanner uses ANSI SQL 2011 with extensions.

 

16. Which database service offers transactional consistency at global scale?

    Cloud Spanner. Cloud Spanner offers transactional consistency at global scale.

 

17. How are Cloud Datastore and Cloud Bigtable alike? Choose all that are correct (2 correct answers)

    They are both highly scalable.

    They are both NoSQL databases.

 

18. True or false: Cloud Datastore databases can span App Engine and Compute Engine applications.

    TRUE

 

Containers in the Cloud

 

Containers:

-   A Hybrid option between IAAS and PAAS, with benefits from both

-   Container gives the independent scalability of workloads (think PAAS) and an abstraction layer of the OS and hardware (think IAAS).

 

Kubernetes:

-   Kubernetes allows to group containers each performing their own function like microservices.

-   Kubernetes makes it easy to orchestrate many containers on many hosts, scale them as microservices, and deploy rollouts and rollbacks.

-   At the core, it’s a set of APIs that can be used to deploy containers on a set of nodes called cluster.

-   Within each container, there is one Master and many other nodes.

-   In Kubernetes, a node represents a computing instance like a machine. In GCP, it’s compute engine VMs.

 

Building Container:

-   Using Docker

-   Using Google Container Builder

-   Steps:

o   Create DockerFile

o   > docker build –t py-server .

o   > docker run –d py-server

 

GKE:

-   GKE is hosted Kubernetes by Google.

-   GKE clusters can be customized, they can support different machine types, numbers of nodes, and network settings.

 

Start kubernetes on a cluster in GKE:

Ø  gcloud container clusters create k1

 

Pod:

-   Wrapper around 1 or more containers

-   A pod is the smallest unit in Kubernetes that you create or deploy.

 

 

Q&A:

1. True or false: each container has its own instance of an operating system.

   Containers start much faster than virtual machines and use fewer resources, because each container does not have its own instance of the operating system.

 

2. Containers are loosely coupled to their environments. What does that mean? Choose all the statements that are true. (3 correct answers)

   Containers abstract away unimportant details of their environments.

   Containers are easy to move around.

   Deploying a containerized application consumes less resources and is less error-prone than deploying an application in virtual machines.

 

   Also, note that Containers need a lightweight container runtime, which does the plumbing jobs needed to allow that container to launch and run. The container runtime also determines the image format.

 

 

App Engine (GCP PAAS)

 

App Engine:

-   App Engine offers NoSQL databases, in-memory caching, load balancing, health checks, logging, and user authentication to applications running in it.

-   App Engine will scale your application automatically in response to the amount of traffic it receives. That’s why App Engine is especially suited for applications where the workload is highly variable, like a web application.

-    

 

App Engine Environment:

-   Standard:

o   Simpler deployment experience

o   Fine-grained auto scaling

-   Flexible:

o   weqqw

 
