[TOC]

# Overview

- About AWS
    + https://aws.amazon.com/about-aws/
- Documentation: https://docs.aws.amazon.com/index.html
    + All AWS tools and services
- AWS Whitepapers and Guides
    + https://aws.amazon.com/whitepapers

# Global Infrastructure

- https://www.youtube.com/watch?v=uj7Ting6Ckk
- https://aws.amazon.com/about-aws/global-infrastructure/
- https://www.rackspace.com/blog/aws-101-regions-availability-zones
- Global AWS services
    + Amazon CloudFront
    + Amazon Route 53
    + Amazon IAM: permission changes in one region are automatically
      copied to all regions
- Partially Global
    + S3: names are global, but physical space is regional

# AWS General

- https://docs.aws.amazon.com/general/latest/gr/Welcome.html
- Shared responsibility model between AWS and customers
    + https://aws.amazon.com/compliance/shared-responsibility-model/
    + AWS: security of the cloud
    + Customers: security in the cloud

## AWS security credentials

When you interact with AWS, you specify your AWS security credentials to
verify who you are (authentication) and whether you have permission
(authorization) to access the resources that you are requesting.

### AWS users

Two types of users in AWS
- Account owner (root user)
    + It is created when the AWS account is created
- AWS Identity and Access Management (IAM) user
    + These users are created by the root user or an IAM administrator
      for the account

Root user credentials
- The credentials of the account owner allow full access to all
  resources in the account.
- You cannot use IAM policies to explicitly deny the root user access to
  resources.
    + You can only use an AWS Organizations service control policy (SCP)
      to limit the permissions of the root user.
    + Because of this, you should create an IAM user with administrator
      permissions to use for everyday AWS tasks and lock away the access
      key for the root user.
- There are specific tasks tasks that are restricted to the AWS account
  root user.
    + Change some of your account settings: this includes the account
      name, email address, root user password, and root user access
      keys.
    + Restore IAM user permissions: if the only IAM administrator
      accidentally revokes their own permissions, you can sign in as the
      root user to edit policies and restore those permissions.
    + Activate IAM access to the Billing and Cost Management console
    + View certain tax invoices.
    + Close your AWS account
    + Change your AWS Support plan or Cancel your AWS Support pan
    + Register as a seller
    + Configure an Amazon S3 bucket to enable MFA Delete.
    + Edit or delete an Amazon S3 bucket policy that includes an invalid
      VPC ID or VPC endpoint ID.
    + Sign up for GovCloud


IAM credentials
- You can create multiple users with different policies that are
  associated with that IAM users.

### AWS credentials

Types of security credentials
- A user name and password to sign in to the AWS Management Console
- Access keys to make programmatic calls to AWS or to use the AWS CLI or
  AWS Tools for PowerShell.

Be sure to save the following credentials (you CANNOT recover these):
- The email address associated with your AWS account
- The AWS account ID
- Your password
- Your secret access keys

(AWS Management) Console access
- Root user: user name and password
- IAM users: account id or account alias, and password
- You can enable MFA for users

Programmatic access
- Access key ID: e.g., `AKIAIOSFODNN7EXAMPLE`
- Secret access key: e.g., `wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY`
    + Only available for download when you create it
    + You must create new access keys if you lose your secret access key
      since there is no way to recover it
- You can assign up to 2 access keys per user
    + 2 access keys are useful for key rotation
    + When you disable an access key, you can't use it, but it counts
      toward your limit of two access keys.

Temporary access keys
- An access key, a secret access key, and a security token that you must
  send to AWS
- https://awscli.amazonaws.com/v2/documentation/api/latest/reference/sts/assume-role.html

```
aws sts assume-role --role-arn arn:aws:iam::634008152794:role/IibsAdminAccess-DO-NOT-DELETE --role-session-name sandop-dataingestion-prod-admin
```

### AWS account identifiers

- AWS account ID: a 12-digit number that uniquely identifies an AWS
  account.
    + `aws sts get-caller-identity --query Account --output text`
- Canonical user ID: an alpha-numeric identifier, such as `79a59df900b949e55d96a1e698fbacedfd6e09d98eacf8f8d5218e7cd47ef2be`.
  That is an obfuscated form of the AWS account ID.
    + You can use this ID to identify an AWS account when granting
      cross-account access to buckets and objects using Amazon S3.
    + https://docs.aws.amazon.com/AmazonS3/latest/userguide/finding-canonical-user-id.html
    + `aws s3api list-buckets --query Owner.ID --output text`

## AWS resources

### Managing AWS Regions

- https://docs.aws.amazon.com/general/latest/gr/rande-manage.html
- Enable/disable a region

### AWS Services endpoints

- https://docs.aws.amazon.com/general/latest/gr/rande.html

### AWS Services quotas

- https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html

### Tagging AWS Resources

- https://docs.aws.amazon.com/general/latest/gr/aws_tagging.html
- You can assign metadata to your AWS resources in the form of tags.
    + Each tag is a label consisting of a user-defined key and value.
    + Tags can help you manage, identify, organize, search for, and
      filter resources.
    + You can create tags to categorize resources by purpose, owner,
      environment, or other criteria.
- Best practices
    + https://docs.aws.amazon.com/whitepapers/latest/tagging-best-practices/tagging-best-practices.html
    + Hierarchical, from `highest-level:to-lower-level:lowest-level`

### Amazon Resource Names  (ARNs)

- https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html
- Amazon Resource Names (ARNs) uniquely identify AWS resources.
    + We require an ARN when you need to specify a resource
      unambiguously across all of AWS, such as in IAM policies, Amazon
      Relational Database Service (Amazon RDS) tags, and API calls.

```
arn:partition:service:region:account-id:resource-id
arn:partition:service:region:account-id:resource-type/resource-id
arn:partition:service:region:account-id:resource-type:resource-id
```

- `partition`: `aws`, `aws-cn`, `aws-us-gov`
- `service`: `s3`, etc.
- `region`: `us-west-2`, etc.
- `account-id`
- `resource-id`

## AWS IP address ranges

- https://docs.aws.amazon.com/general/latest/gr/aws-ip-ranges.html

## AWS APIs

### API retries

- Error retry and exponential backoff strategy
- https://docs.aws.amazon.com/general/latest/gr/api-retries.html

### Signing AWS API Requests

- https://docs.aws.amazon.com/general/latest/gr/signing_aws_api_requests.html
- This is useful if you want to write your own AWS SDK to send AWS API
  requests.

### AWS SDK support for Amazon S3 client-side encryption

- https://docs.aws.amazon.com/general/latest/gr/aws_sdk_cryptography.html

# AWS SDK

- Python
    + https://aws.amazon.com/sdk-for-python/
    + https://github.com/boto/boto3
    +

# AWS Products

- Fargate vs. ECS vs. EKS
    + https://spot.io/blog/fargate-vs-ecs-comparing-amazons-container-management-services/
- Load balancer
    + ALB (Application LB), NLB (Network LB), GLB (Gateway Load
      Balancer), Global Accelerator
        * https://youtu.be/p0YZBF03r5A?si=xWEc4pkraUq81BNr


# Tips and Tricks

## Auto shutdown and start AWS instance

- http://www.4synergy.nl/auto-start-stop-ec2-instances/
- Use python [boto](http://boto.readthedocs.org/en/latest/) package to
  manipulate with AWS instance.
- http://stackoverflow.com/questions/2413029/auto-shutdown-and-start-amazon-ec2-instance
