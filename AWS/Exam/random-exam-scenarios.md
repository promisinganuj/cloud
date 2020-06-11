### **Question 1**
User in Account A wants to read the SQS queue in his account and save those messages in S3 bucket in Account B. What is the best way to design such a solution?

**Solution:**
* We need to grant access to user in Account A via a bucket policy in account B.
* Typically, we would think that we should create a role in account B and user in account A should assume that instead of granting direct access through bucket policies. But this solution won't work in this case as the user needs to have access to resouces in both account A and account B.
* Remember that when any identity assumes a role, it gives away it's existing privileges and works on the privileges assigned to the role only. In our case, once the user assumes the role in account B, he/she wouldn't be able to access resouces in account A.

### **Question 2**
An education company delivers course materials to their students as PDF downloads. Recently, there have been more downloads than students in their classes, and the company wants to limit each PDF to being downloaded to class members.

The current architecture has students log in to a website that runs on EC2 instances. The website provides links to publicly accessible files in Amazon S3. The company wants to use CloudFront to limit the downloads.

**Solution:**
* Configure CloudFront with an OAI for Amazon S3, and remove public read actions from the S3 bucket policy. Createa CloudFront behavior with the AWS account as trusted signer. Have the web servers return a CloudFront-signed URL.
* Please note that you can't have an EC2 role for the web servers that can explicitly deny all Amazon S3 actions.

### **Question 3**
You are working with a company that wants to create a new game using AWS Mobile Hub. Backend systems will use multiple AWS Regions. Player data, including scores, will be stored in the region closest to users when the game is first launched.

Each region is to host its own scoreboard. Company leaders want scoreboards in each region to display high scores from both the Region and those achieved globally. In each region, how should the backend store player score information?

**Solution:**
* Writer scores to a DynamoDB table in the local region. Enable DynamoDB streams, create a worker tier to consume the stream, and replay the data to DynamoDB tables in all other regions.
* or use DynamoDB Global Tables
* Please note here that Aurora can't replicate a single table. Also, it can only have 1 cross-region read replica.

### **Question 4**
You are working with a company that collects clickstream data from global web-based marketing campaigns. The system uses Auto Scaling with Amazon EC2 instances behind an ELB load balancer. Data is stored using MySQL RDS. A single campaign lasts between one and two weeks. When complete, the tracking system is deleted to minimize cost.

Quarterly, data from every campaign is moved to Amazon Redshift for aggregation, analysis, and detailed reporting. The company adopted AWS CloudFormation to automatically deploy the application in any region.

How can you ensure that the AWS CloudFormation template meets the customer’s requirements?  Select two answers. 

**Solution:**
* Use mappings and the Fn::FindInMap function to find the right AMI ID for the ImageId attibute.
* Set a DeletionPolicy of Snapshot for the RDS instances.
* Note that a DeletionPolicy of Snapshot takes a snapshot of the Amazon RDS database before deleting it.

### **Question 5**
You have a client that has an application with components written in various languages, including Ruby, Node.js, and PHP. Data is stored in an Amazon RDS MySQL database. Logs from the components contain different fields and information. Your task is to centralize the logs and use them to produce a coherent weekly report of usage patterns.

What approach should you take?

**Solution:**
* Have each application put its logs in Amazon S3. Process the logs using Amazon EMR, and store the results in Amazon Redshift for long-term analysis using various BI tools.
* Please note here that Redshift is not optimal for real time data ingestion. So, using Amazon kinesis to ingest logs into Amazon Redshift in real time would be a sub-optimal choice.

### **Question 6**
A new mobile app has been developed by one of your clients to update an Amazon DynamoDB table with temperature readings. The goal is to support tens of thousands of users by the end of the year. One of the security requirements for this app dictates that anonymous logins are not allowed.

How would you architect the mobile app to gain credentials to update the database?

**Solution:**
* Use an Amazon Cognito user pool for authentication and create a role allowing updates to the DynamoDB table. Have the mobile app use Amazon Cognito identity pools to retrieve temporary credentials.
* Please note that Amazon identity pools support anonymous guest users so using Amazon identity pool for authentication is not suitable in this scenario.

* User Pools:
  * Provides a directory profile for all users which you can access through an SDK.
  * Supports user federation through a third-party identity provider. 
  * Signed users receive authentication tokens.
  * Tokens can be exchanged for AWS access via Amazon Cognito identity pools.

* Identity Pools:
  * Authenticates users with web identity providers, including Amazon Cognito user pools.
  * Assigns temporary AWS credentials via AWS STS.
Supports anonymous guest users.

### **Question 7**
Suspicious activity involving AWS account root user credentials has been noticed by one of your clients via AWS CloudTrail. Going forward, the client’s security officer wants to be notified of any other logged API activity involving root access keys across all three regions. He also wants to quickly access these logs from one location at the lowest cost possible. Log integrity must be verified in case of tampering.

Which of the following is the best solution to meet the security officer’s requests?

**Solution:**
* Create a trail in each region and configure them to send logs to a single S3 bucket. Configure CloudWatch alarms to send Amazon SNS notifications for root access key activity. Enable CloudTrail log file integrity validation.

### **Question 8**
A software company is considering Elastic Beanstalk to deploy new versions of their applications into their production environment consisting of a Multi-AZ RDS setup. Application availability during deployment and a low-cost solution are top priorities. After the deployment, the company is required to delete the source application code used by Elastic Beanstalk.

What would you recommend for a deployment solution?

**Solution:**
* Run a rolling deployment to minimize application downtime and manually delete the source bundle after the deployment.

### **Question 9**
1. Does your compute layer require the **lowest latency** and **highest packet-per-second network performance possible**?
2. Do your applications that have a small number of **critical instances that should be kept separate** from each other?
3. Do you have **large distributed and replicated workloads** such as HDFS, HBase and Cassandra running on EC2?

**Solution:**
1. Cluster Placement Group
* The cluster placement group is a logical grouping of instances within a **single Availability Zone**.
* This grouping provides the lowest latency and highest packet per second network performance.

2. Spread Placement Group
* A spread placement group is a grouping of instances that are purposely positioned on distinct underlying hardware. * This grouping reduces the risk of simultaneous failures that could occur if instances were sharing underlying hardware

* **This type of group can span multiple Availability Zones**, up to a maximum of seven instances per Availability Zone per group.

* Spread placement groups help reduce the likelihood of failures within clusters or groups of instances.

3. Partition Plaecment Group
* Partition placement groups spread EC2 instances across logical partitions and ensure that instances in different partitions do not share the same underlying hardware, thus containing the impact of hardware failure to a single partition.

### **Question 10**
