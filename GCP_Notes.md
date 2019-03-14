# Google Cloud Platform (GCP)
## Four Kinds of Services on GCP
1. Compute
- Compute Engine
- Kubernetes Engine
- App Engine
- Cloud Functions
2. Storage
- Bigtable
- Cloud Storage
- Cloud SQL
- Cloud Spanner
- Cloud Datastore
3. Big Data
- Big Query
- Pub/Sub
- Data flow
- Data proc
- Data lab
4. Machine Learning
- Natural Language API
- Vision API
- Machine Learning
- Speech API
- Translate API

Along with Network VPCs (Virtual Private Cloud)

## Standard Definition of Cloud (Provided by US National Institute of Standards and Technology)
- On-demand Self Service: No human intervention needed to get resources
- Broad Network Acces: Access from anywhere
- Resouce Pooling: Provider shares resources to customer. Economy of Scale
- Rapid Elasticity: Get more resources quickly as needed
- Measured Services: Pay only for what you consume. Pay-as-you-go (PAYG) model

## The journey so far
- Physical/Colocation: User-configured, managed and maintained
- Virtualization: User-configured, provider-managed and maintained
- Serverless: Fully automated

## Infrastructure as a Service (IAAS)
- Raw Compute, Netword and Storage
- Pay for what you allocated

## Platform as a Service (PAAS)
- Bind application code to libraries that give access to the infrastructure the application needs.
- Pay for what you use

## A rough sketch of GCP Architecure
- Compute Engine - IAAS
- Kubernetes Engine - Hybrid
- App Engine - PAAS
- Cloud Functions - Serverless Logic
- Managed Services - Automated elastic resources

## GCP Regions and Zones
Multi-Region (min seperation of 160 km) -> Region (Independent Geographic Areas) -> Zone

## GCP Resource Hierarchy
Org Node -> Folders -> Projects -> Resources

### Org Node
- Top of the hierarchy
- Special Roles such as "Organization Policy Administrator" and "Project Creator"

## Identity and Access Management (IAM)
- Who: Google Account, Cloud Identity User, Service Account, Google Group, Cloud Identity or G Suite domain
- Can do what
- On which resource

### IAM Role Types
- Primitive: Owner, Editor, Viewer, Billing Administrator. Too Coarse
- Predefined: Applies to a particular GCP service in a project. Fine Grained
- Custom: Most Granularity

## Interacting with GCP
- Cloud Platform Console - Web User Interface
- Cloud Shell and Cloud SPD - CPI
- Cloud Console Mobile App - iOS, Android
- REST-based API - For custom applications



