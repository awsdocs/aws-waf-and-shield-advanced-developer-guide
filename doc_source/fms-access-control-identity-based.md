# Using identity\-based policies \(IAM policies\) for AWS Firewall Manager<a name="fms-access-control-identity-based"></a>

This section provides examples of identity\-based policies that demonstrate how an account administrator can attach permissions policies to IAM identities \(that is, users, groups, and roles\) and thereby grant permissions to perform operations on AWS Firewall Manager resources\. 

**Important**  
We recommend that you first review the introductory topics that explain the basic concepts and options available for you to manage access to your AWS Firewall Manager resources\. For more information, see [Overview of managing access permissions to your AWS Firewall Manager resources](fms-access-control-overview.md)\.

For a table that shows all the AWS Firewall Manager API actions and the resources that they apply to, see [Firewall Manager required permissions for API actions](fms-api-permissions-ref.md)\. 

## Topics<a name="fms-topics3"></a>
+ [Permissions required to use the AWS Firewall Manager console](#fms-additional-console-required-permissions)
+ [AWS managed \(predefined\) policies for AWS Firewall Manager](#fms-access-policy-examples-aws-managed) 
+ [Customer managed policy examples](#fms-access-policy-examples-for-sdk-cli) 

## Permissions required to use the AWS Firewall Manager console<a name="fms-additional-console-required-permissions"></a>

The AWS Firewall Manager console provides an integrated environment for you to create and manage Firewall Manager resources\. The console provides many features and workflows that often require permissions to create a Firewall Manager resource in addition to the API\-specific permissions that are documented in the [Firewall Manager required permissions for API actions](fms-api-permissions-ref.md)\. For more information about these additional console permissions, see [Customer managed policy examples](#fms-access-policy-examples-for-sdk-cli)\.

## AWS managed \(predefined\) policies for AWS Firewall Manager<a name="fms-access-policy-examples-aws-managed"></a>

AWS addresses many common use cases by providing standalone IAM policies that are created and administered by AWS\. Managed policies grant necessary permissions for common use cases so you can avoid having to investigate what permissions are needed\. For more information, see [AWS Managed Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

The following AWS managed policies, which you can attach to users in your account, are specific to AWS Firewall Manager and are grouped by use case scenario:
+ `AWSFMAdminFullAccess` – Grants full access to AWS Firewall Manager resources\.
+ `AWSFMAdminReadOnlyAccess` – Grants read\-only access to all AWS Firewall Manager resources\. 
+ `AWSFMMemberReadOnlyAccess` – Grants read\-only access to AWS Firewall Manager member resources\. 

**Note**  
You can review these permissions policies by signing in to the IAM console and searching for specific policies there\.

You also can create your own custom IAM policies to allow permissions for AWS Firewall Manager API operations and resources\. You can attach these custom policies to the IAM users or groups that require those permissions or to custom execution roles \(IAM roles\) that you create for your Firewall Manager resources\. 

## Customer managed policy examples<a name="fms-access-policy-examples-for-sdk-cli"></a>

The examples in this section provide a group of sample policies that you can attach to a user\. If you are new to creating policies, we recommend that you first create an IAM user in your account and attach the policies to the user, in the sequence outlined in the steps in this section\.

You can use the console to verify the effects of each policy as you attach the policy to the user\. Initially, the user doesn't have permissions, and the user won't be able to do anything on the console\. As you attach policies to the user, you can verify that the user can perform various operations on the console\. 

We recommend that you use two browser windows: one to create the user and grant permissions, and the other to sign in to the AWS Management Console using the user's credentials and verify permissions as you grant them to the user\.

For examples that show how to create an IAM role that you can use as an execution role for your Firewall Manager resource, see [Creating IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create.html) in the *IAM User Guide*\.

### Example topics<a name="fms-topics4"></a>
+ [Example: Give admin user read\-only access to Firewall Manager security groups](#fms-example1)

### Create an IAM user<a name="fms-console-permissions-list-functions"></a>

First, you need to create an IAM user, add the user to an IAM group with administrative permissions, and then grant administrative permissions to the IAM user that you created\. You then can access AWS using a special URL and the user's credentials\. 

For instructions, see [Creating Your First IAM User and Administrators Group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html) in the *IAM User Guide*\. 

### Example: Give admin user read\-only access to Firewall Manager security groups<a name="fms-example1"></a>

The following policy grants admin users read\-only access to Firewall Manager security groups and policies\. These users can't create, update, or delete the Firewall Manager resources\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "fms:Get*",
                "fms:List*",
                "ec2:DescribeSecurityGroups"
            ],
            "Effect": "Allow",
            "Resource": "*"
        }
    ]
}
```