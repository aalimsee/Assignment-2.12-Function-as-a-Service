# Assignment 2.12 Function as a Service

Assignment:
Given a Lambda function that is triggered upon the creation of files in an S3 bucket, answer the following:

What is the purpose of the execution role on the Lambda function? 
Ans: The execution role on an AWS Lambda function is an Identity and Access Management (IAM) role that defines the permissions a Lambda function has to access other AWS services and resources, essentially controlling what actions the function can perform when it is invoked; ensuring that the function only has the minimum permissions needed to execute its task, following the principle of least privilege

What is the purpose of the resource-based policy on the Lambda function?
Ans: A resource-based policy on an AWS Lambda function controls which other AWS services or accounts can invoke (execute) that function, essentially defining who has permission to access and trigger the Lambda function, allowing for fine-grained access control beyond just the user identity associated with the function itself; this is done by specifying which services or accounts are allowed to call the function and under what conditions. 

If the function is needed to upload a file into an S3 bucket, describe (i.e no need for the actual policies)
1. What is the needed update on the execution role?
2. What is the new resource-based policy that needs to be added (if any)?

Ans: 
If a function (such as an AWS Lambda function) needs to upload a file to an S3 bucket, here are the required updates:

1. Update Execution Role (IAM Role for Lambda /or EC2)

The IAM role associated with the function needs permissions to write to S3. Specifically, the role should have:
s3:PutObject permission for the target bucket (to upload files).
s3:GetObject permission (if the function also needs to read files after uploading).
s3:ListBucket (optional, if the function needs to check existing objects in the bucket).
The IAM policy should specify the S3 bucket ARN and the necessary object key prefixes (if applicable) to avoid overly broad permissions.

2. Resource-Based Policy (S3 Bucket Policy)
A new S3 bucket policy is needed only if the function’s execution role belongs to a different AWS account or if fine-grained access control is required. The policy should:
Allow s3:PutObject for the function’s IAM role (Principal: { "AWS": "execution-role-ARN" }).
Optionally, allow s3:ListBucket if needed.
Restrict access to specific prefixes or object keys if necessary.
Ensure s3:PutObjectAcl is included only if the function needs to set object ACLs.
If the function and the S3 bucket are in the same AWS account, an S3 bucket policy is not mandatory, as long as the IAM execution role has the correct permissions.


Create a public github repository that has a README.md file, containing the above answers.
Submission is the url to your public github repository.
