[TOC]

# Overview

- Documentation: https://docs.aws.amazon.com/index.html
    + All AWS tools and services

# AWS General

- https://docs.aws.amazon.com/general/latest/gr/Welcome.html

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

# AWS CLI

- User Guide
    + https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html
- Installation
    + https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

# AWS SDK

- Python
    + https://aws.amazon.com/sdk-for-python/
    + https://github.com/boto/boto3
    +

# Tips and Tricks

## Auto shutdown and start AWS instance

- http://www.4synergy.nl/auto-start-stop-ec2-instances/
- Use python [boto](http://boto.readthedocs.org/en/latest/) package to
  manipulate with AWS instance.
- http://stackoverflow.com/questions/2413029/auto-shutdown-and-start-amazon-ec2-instance
