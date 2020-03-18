**Q1.** User in Account A wants to read the SQS queue in his account and save those messages in S3 bucket in Account B. What is the best way to design such a solution?

**Solution:**
* We need to grant access to user in Account A via a bucket policy in account B.
* Typically, we would think that we should create a role in account B and user in account A should assume that instead of granting direct access through bucket policies. But this solution won't work in this case as the user needs to have access to resouces in both account A and account B.
* Remember that when any identity assumes a role, it gives away it's existing privileges and works on the privileges assigned to the role only. In our case, once the user assumes the role in account B, he/she wouldn't be able to access resouces in account A.
