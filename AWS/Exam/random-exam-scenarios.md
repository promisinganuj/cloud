**Q1.** User in Account A wants to read the SQS queue in his account and save those messages in S3 bucket in Account B. What is the best way to design such a solution?

**Solution:**
* We need to grant access to user in Account A via a bucket policy in account B.
* Typically, we would think that we should create a role in account B and user in account A should assume that instead of granting direct access through bucket policies. But this solution won't work in this case as the user needs to have access to resouces in both account A and account B.
* Remember that when any identity assumes a role, it gives away it's existing privileges and works on the privileges assigned to the role only. In our case, once the user assumes the role in account B, he/she wouldn't be able to access resouces in account A.

**Q1.** An education company delivers course materials to their students as PDF downloads. Recently, there have been more downloads than students in their classes, and the company wants to limit each PDF to being downloaded to class members.

The current architecture has students log in to a website that runs on EC2 instances. The website provides links to publicly accessible files in Amazon S3. The company wants to use CloudFront to limit the downloads.

**Solution:**
* Configure CloudFront with an OAI for Amazon S3, and remove public read actions from the S3 bucket policy. Createa CloudFront behavior with the AWS account as trusted signer. Have the web servers return a CloudFront-signed URL.
* Please note that you can't have an EC2 role for the web servers that can explicitly deny all Amazon S3 actions.
