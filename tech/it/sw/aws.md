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
