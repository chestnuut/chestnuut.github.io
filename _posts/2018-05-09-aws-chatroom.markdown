
`This article is for a course on udemy: build a serveless app on AWS`

# Steps:
1. Create AWS S3 to store HTML, CSS, Javascript files.
2. Create IAM policies to grant access of interacting with Lambda services and S3 services.
3. In create policy tab, select the bucket you wish to create, and store.
4. Then create a role to use that policy. In this project, we should use Lambda service to use that policy. [Besides this policy, we also need to add *AWSLambdaBasicExcecutionRole* policy]
5. 


# AWS S3
S3 = simple storage service. A Key Blob store.
A system for storing blobs(二进制大型对象) of data, those blobs are associated with unique key names.
- Eventually Consistant
- Extremely durable
- Is not a file system.

## A file system
A file system operations tend to be atomic.
Atomic: when you write something it's immediately available to be read back.

### **V1** set up S3 and upload static page on web.

### **V2** update aws policy to grant permission GetObject

A JSON object

	{
	  "Version": "2012-10-17",
	  "Id": "Policy1497053408897",
	  "Statement": [
	    {
	      "Sid": "Stmt1497053406813",
	      "Effect": "Allow",
	      "Principal": "*",
	      "Action": "s3:GetObject",
	      "Resource": "arn:aws:s3:::<your bucket name>/*"
	    }
	  ]
	}

# AWS Lambda

Difference between AWS lambda ans AWS EC2.
Lambda is more efficient

# AWS IAM

IAM: Identity and Access Management service

 - Users/Groups
 - roles
 - policies
 - something else...

ARN: Amazon Resource Name


 
