# Using identity\-based policies \(IAM policies\) for AWS WAF Classic<a name="classic-access-control-identity-based"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

This section provides examples of identity\-based policies that demonstrate how an account administrator can attach permissions policies to IAM identities \(that is, users, groups, and roles\) and thereby grant permissions to perform operations on AWS WAF Classic resources\. 

**Important**  
We recommend that you first review the introductory topics that explain the basic concepts and options available for you to manage access to your AWS WAF Classic resources\. For more information, see [Overview of managing access permissions to your AWS WAF Classic resources](classic-access-control-overview.md)\.

The following shows an example of a permissions policy:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "CreateFunctionPermissions",
            "Effect": "Allow",
            "Action": [
                "waf:ListWebACLs",               
                "waf:ListRules",               
                "waf:GetWebACL",               
                "waf:GetRule",               
                "cloudwatch:ListMetrics",
                "waf:GetSampledRequests"
            ],
            "Resource": "*"
        },
        {
            "Sid": "PermissionToPassAnyRole",
            "Effect": "Allow",
            "Action": [
                "iam:PassRole"
            ],
            "Resource": "arn:aws:iam::account-id:role/*"
        }
    ]
}
```

 The policy has two statements: 
+ The first statement grants permissions to view statistics for AWS WAF Classic web ACLs, using the `waf:ListWebACLs`, `waf:ListRules`, `waf:GetWebACL`, `waf:GetRule`, `cloudwatch:ListMetrics`, and `waf:GetSampledRequests` actions\. AWS WAF Classic doesn't support permissions for some of these actions at the resource level\. Therefore, the policy specifies a wildcard character \(\*\) as the `Resource` value\. 
+ The second statement grants permissions for the IAM action `iam:PassRole` on IAM roles\. The wildcard character \(\*\) at the end of the `Resource` value means that the statement allows permissions for the `iam:PassRole` action on any IAM role\. To only extend these permissions to a specific role, replace the wildcard character \(\*\) in the resource ARN with the specific role name\. 

The policy doesn't specify the `Principal` element because in an identity\-based policy you don't specify the principal who gets the permissions\. When you attach a policy to a user, the user is the implicit principal\. When you attach a permissions policy to an IAM role, the principal identified in the role's trust policy gets the permissions\.

For a table that shows all the AWS WAF Classic API actions and the resources that they apply to, see [AWS WAF Classic API permissions: Actions, resources, and conditions reference](classic-waf-api-permissions-ref.md)\. 

## Topics<a name="classic-topics3"></a>
+ [Permissions required to use the AWS WAF Classic console](#classic-additional-console-required-permissions)
+ [AWS managed \(predefined\) policies for AWS WAF Classic](#classic-access-policy-examples-aws-managed) 
+ [Customer managed policy examples](#classic-access-policy-examples-for-sdk-cli) 

## Permissions required to use the AWS WAF Classic console<a name="classic-additional-console-required-permissions"></a>

The AWS WAF Classic console provides an integrated environment for you to create and manage AWS WAF Classic resources\. The console provides many features and workflows that often require permissions to create an AWS WAF Classic resource in addition to the API\-specific permissions that are documented in the [AWS WAF Classic API permissions: Actions, resources, and conditions reference](classic-waf-api-permissions-ref.md)\. For more information about these additional console permissions, see [Customer managed policy examples](#classic-access-policy-examples-for-sdk-cli)\.

## AWS managed \(predefined\) policies for AWS WAF Classic<a name="classic-access-policy-examples-aws-managed"></a>

AWS addresses many common use cases by providing standalone IAM policies that are created and administered by AWS\. Managed policies grant necessary permissions for common use cases so you can avoid having to investigate what permissions are needed\. For more information, see [AWS Managed Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

The following AWS managed policies, which you can attach to users in your account, are specific to AWS WAF Classic:
+ `AWSWAFReadOnlyAccess` – Grants read\-only access to AWS WAF Classic resources\. 
+ `AWSWAFFullAccess` – Grants full access to AWS WAF Classic resources\.
+ `AWSWAFConsoleReadOnlyAccess` – Grants read\-only access to the AWS WAF Classic console, which includes resources for AWS WAF and integrated services, such as Amazon CloudFront, Amazon API Gateway, Application Load Balancer, and Amazon CloudWatch\. 
+ `AWSWAFConsoleFullAccess` – Grants full access to the AWS WAF Classic console, which includes resources for AWS WAF and integrated services, such as Amazon CloudFront, Amazon API Gateway, Application Load Balancer, and Amazon CloudWatch\. 

**Note**  
You can review these permissions policies by signing in to the IAM console and searching for specific policies there\.

You also can create your own custom IAM policies to allow permissions for AWS WAF Classic API operations and resources\. You can attach these custom policies to the IAM users or groups that require those permissions or to custom execution roles \(IAM roles\) that you create for your AWS WAF Classic resources\. 

## Customer managed policy examples<a name="classic-access-policy-examples-for-sdk-cli"></a>

The examples in this section provide a group of sample policies that you can attach to a user\. If you are new to creating policies, we recommend that you first create an IAM user in your account and attach the policies to the user, in the sequence outlined in the steps in this section\.

You can use the console to verify the effects of each policy as you attach the policy to the user\. Initially, the user doesn't have permissions, and the user won't be able to do anything on the console\. As you attach policies to the user, you can verify that the user can perform various operations on the console\. 

We recommend that you use two browser windows: one to create the user and grant permissions, and the other to sign in to the AWS Management Console using the user's credentials and verify permissions as you grant them to the user\.

For examples that show how to create an IAM role that you can use as an execution role for your AWS WAF Classic resource, see [Creating IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create.html) in the *IAM User Guide*\.

### Example topics<a name="classic-topics4"></a>
+ [Example 1: Give users read\-only access to AWS WAF Classic, CloudFront, and CloudWatch](#classic-example1)
+ [Example 2: Give users full access to AWS WAF Classic, CloudFront, and CloudWatch](#classic-example2) 
+ [Example 3: Granting access to a specified AWS account](#classic-example3) 
+ [Example 4: Granting access to a specified Web ACL](#classic-example4) 

### Create an IAM user<a name="classic-console-permissions-list-functions"></a>

First, you need to create an IAM user, add the user to an IAM group with administrative permissions, and then grant administrative permissions to the IAM user that you created\. You then can access AWS using a special URL and the user's credentials\. 

For instructions, see [Creating Your First IAM User and Administrators Group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html) in the *IAM User Guide*\. 

### Example 1: Give users read\-only access to AWS WAF Classic, CloudFront, and CloudWatch<a name="classic-example1"></a>

The following policy grants users read\-only access to AWS WAF Classic resources, to Amazon CloudFront web distributions, and to Amazon CloudWatch metrics\. It's useful for users who need permission to view the settings in AWS WAF Classic conditions, rules, and web ACLs to see which distribution is associated with a web ACL, and to monitor metrics and a sample of requests in CloudWatch\. These users can't create, update, or delete AWS WAF Classic resources\.

```
{
   "Version":"2012-10-17",
   "Statement": [
      {
         "Action": [
            "waf:Get*",
            "waf:List*",
            "cloudfront:GetDistribution",
            "cloudfront:GetDistributionConfig",
            "cloudfront:ListDistributions",
            "cloudfront:ListDistributionsByWebACLId",
            "cloudwatch:ListMetrics",
            "cloudwatch:GetMetricStatistics"
         ],
         "Effect": "Allow",
         "Resource": "*"
      }
   ]
}
```

### Example 2: Give users full access to AWS WAF Classic, CloudFront, and CloudWatch<a name="classic-example2"></a>

The following policy lets users perform any AWS WAF Classic operation, perform any operation on CloudFront web distributions, and monitor metrics and a sample of requests in CloudWatch\. It's useful for users who are AWS WAF Classic administrators\.

```
{
   "Version": "2012-10-17",
   "Statement": [
      {
         "Action": [
            "waf:*",
            "cloudfront:CreateDistribution",
            "cloudfront:GetDistribution",
            "cloudfront:GetDistributionConfig",
            "cloudfront:UpdateDistribution",
            "cloudfront:ListDistributions",
            "cloudfront:ListDistributionsByWebACLId",
            "cloudfront:DeleteDistribution",
            "cloudwatch:ListMetrics",
            "cloudwatch:GetMetricStatistics"
         ],
         "Effect": "Allow",
         "Resource": "*"
      }
   ]
}
```

We strongly recommend that you configure multi\-factor authentication \(MFA\) for users who have administrative permissions\. For more information, see [Using Multi\-Factor Authentication \(MFA\) Devices with AWS](https://docs.aws.amazon.com/IAM/latest/UserGuide/Using_ManagingMFA.html) in the *IAM User Guide*\. 

### Example 3: Granting access to a specified AWS account<a name="classic-example3"></a>

This policy grants the following permissions to the account 444455556666:
+ Full access to all AWS WAF Classic operations and resources\.
+ Read and update access to all CloudFront distributions, which allows you to associate web ACLs and CloudFront distributions\.
+ Read access to all CloudWatch metrics and metric statistics, so that you can view CloudWatch data and a sample of requests in the AWS WAF Classic console\. 

```
{
   "Version": "2012-10-17",
   "Statement": [
      {
         "Effect": "Allow",
         "Action": [
            "waf:*"
         ],
         "Resource": [
            "arn:aws:waf::444455556666:*"
         ]
      },
      {
         "Effect": "Allow",
         "Action": [
            "cloudfront:GetDistribution",
            "cloudfront:GetDistributionConfig",
            "cloudfront:ListDistributions",
            "cloudfront:ListDistributionsByWebACLId",
            "cloudfront:UpdateDistribution",
            "cloudwatch:ListMetrics",
            "cloudwatch:GetMetricStatistics"
         ],
         "Resource": [
            "*"
         ]
      }
   ]
}
```

### Example 4: Granting access to a specified Web ACL<a name="classic-example4"></a>

This policy grants the following permissions to the `webacl` ID 112233d7c\-86b2\-458b\-af83\-51c51example in the account 444455556666:
+ Full access to AWS WAF Classic `Get`, `Update`, and `Delete` operations and resources

```
{
   "Version": "2012-10-17",
   "Statement": [
      {
         "Effect": "Allow",
         "Action": [
            "waf:*"
         ],
         "Resource": [
            "arn:aws:waf::444455556666:webacl/112233d7c-86b2-458b-af83-51c51example"
         ]
      }
   ]
}
```