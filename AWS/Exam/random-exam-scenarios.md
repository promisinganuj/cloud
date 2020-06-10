**Question 1.** User in Account A wants to read the SQS queue in his account and save those messages in S3 bucket in Account B. What is the best way to design such a solution?

**Solution:**
* We need to grant access to user in Account A via a bucket policy in account B.
* Typically, we would think that we should create a role in account B and user in account A should assume that instead of granting direct access through bucket policies. But this solution won't work in this case as the user needs to have access to resouces in both account A and account B.
* Remember that when any identity assumes a role, it gives away it's existing privileges and works on the privileges assigned to the role only. In our case, once the user assumes the role in account B, he/she wouldn't be able to access resouces in account A.

**Question 2.** An education company delivers course materials to their students as PDF downloads. Recently, there have been more downloads than students in their classes, and the company wants to limit each PDF to being downloaded to class members.

The current architecture has students log in to a website that runs on EC2 instances. The website provides links to publicly accessible files in Amazon S3. The company wants to use CloudFront to limit the downloads.

**Solution:**
* Configure CloudFront with an OAI for Amazon S3, and remove public read actions from the S3 bucket policy. Createa CloudFront behavior with the AWS account as trusted signer. Have the web servers return a CloudFront-signed URL.
* Please note that you can't have an EC2 role for the web servers that can explicitly deny all Amazon S3 actions.

**Question 3**
You are working with a company that wants to create a new game using AWS Mobile Hub. Backend systems will use multiple AWS Regions. Player data, including scores, will be stored in the region closest to users when the game is first launched.

Each region is to host its own scoreboard. Company leaders want scoreboards in each region to display high scores from both the Region and those achieved globally. In each region, how should the backend store player score information?

**Solution:**
* Writer scores to a DynamoDB table in the local region. Enable DynamoDB streams, create a worker tier to consume the stream, and replay the data to DynamoDB tables in all other regions.
* or use DynamoDB Global Tables
* Please note here that Aurora can't replicate a single table. Also, it can only have 1 cross-region read replica.

**Question 4**
You are working with a company that collects clickstream data from global web-based marketing campaigns. The system uses Auto Scaling with Amazon EC2 instances behind an ELB load balancer. Data is stored using MySQL RDS. A single campaign lasts between one and two weeks. When complete, the tracking system is deleted to minimize cost.

Quarterly, data from every campaign is moved to Amazon Redshift for aggregation, analysis, and detailed reporting. The company adopted AWS CloudFormation to automatically deploy the application in any region.

How can you ensure that the AWS CloudFormation template meets the customer’s requirements?  Select two answers. 

**Solution:**
* Use mappings and the Fn::FindInMap function to find the right AMI ID for the ImageId attibute.
* Set a DeletionPolicy of Snapshot for the RDS instances.
* Note that a DeletionPolicy of Snapshot takes a snapshot of the Amazon RDS database before deleting it.

**Question 5**
You have a client that has an application with components written in various languages, including Ruby, Node.js, and PHP. Data is stored in an Amazon RDS MySQL database. Logs from the components contain different fields and information. Your task is to centralize the logs and use them to produce a coherent weekly report of usage patterns.

What approach should you take?

**Solution:**
* Have each application put its logs in Amazon S3. Process the logs using Amazon EMR, and store the results in Amazon Redshift for long-term analysis using various BI tools.
* Please note here that Redshift is not optimal for real time data ingestion. So, using Amazon kinesis to ingest logs into Amazon Redshift in real time would be a sub-optimal choice.
