# Using identity\-based policies \(IAM policies\) for AWS Shield<a name="shd-access-control-identity-based"></a>

This section provides examples of identity\-based policies that demonstrate how an account administrator can attach permissions policies to IAM identities \(that is, users, groups, and roles\) and thereby grant permissions to perform operations on AWS Shield resources\. 

**Important**  
We recommend that you first review the introductory topics that explain the basic concepts and options available for you to manage access to your AWS Shield resources\. For more information, see [Overview of managing access permissions to your AWS Shield resources](shd-access-control-overview.md)\.

The following shows an example of a permissions policy:

```
{
    "Version": "2016-06-02",
    "Statement": [
        {
            "Sid": "CreateFunctionPermissions",
            "Effect": "Allow",
            "Action": [
                "shield:ListProtections",              
                "shield:DescribeProtection", 
                "shield:ListAttacks",
                "shield:DescribeAttack"
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
+ The first statement grants permissions to view statistics for AWS Shield protections and actions\. The policy specifies a wildcard character \(\*\) as the `Resource` value\. 
+ The second statement grants permissions for the IAM action `iam:PassRole` on IAM roles\. The wildcard character \(\*\) at the end of the `Resource` value means that the statement allows permissions for the `iam:PassRole` action on any IAM role\. To only extend these permissions to a specific role, replace the wildcard character \(\*\) in the resource ARN with the specific role name\. 

The policy doesn't specify the `Principal` element because in an identity\-based policy you don't specify the principal who gets the permissions\. When you attach a policy to a user, the user is the implicit principal\. When you attach a permissions policy to an IAM role, the principal identified in the role's trust policy gets the permissions\.

For a table that shows all the AWS Shield API actions and the resources that they apply to, see [Shield required permissions for API actions](shd-api-permissions-ref.md)\. 

## Topics<a name="shd-topics3"></a>
+ [Permissions required to use the AWS Shield console](#shd-additional-console-required-permissions)
+ [AWS managed \(predefined\) policies for AWS Shield](#shd-access-policy-examples-aws-managed) 
+ [Customer managed policy examples](#shd-access-policy-examples-for-sdk-cli) 

## Permissions required to use the AWS Shield console<a name="shd-additional-console-required-permissions"></a>

The AWS Shield console provides an integrated environment for you to create and manage Shield resources\. The console provides many features and workflows that often require permissions to create an Shield resource in addition to the API\-specific permissions that are documented in the [Shield required permissions for API actions](shd-api-permissions-ref.md)\. For more information about these additional console permissions, see [Customer managed policy examples](#shd-access-policy-examples-for-sdk-cli)\.

## AWS managed \(predefined\) policies for AWS Shield<a name="shd-access-policy-examples-aws-managed"></a>

AWS addresses many common use cases by providing standalone IAM policies that are created and administered by AWS\. Managed policies grant necessary permissions for common use cases so you can avoid having to investigate what permissions are needed\. For more information, see [AWS Managed Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

AWS Shield uses the AWS managed policy `AWSShieldDRTAccessPolicy` that you can use to grant the AWS Shield DDoS Response Team \(DRT\) access to your account\. This allows the DRT to perform actions on your account, to manage your AWS WAF rules and Shield protections\. To use this, you create a role and pass it to the Shield API operation, associate DRT role\. In the API, this is `AssociateDRTRole`\. In the CLI, it's `associate-drt-role`\. For more information about this policy, see [Step 5: Configure AWS DRT support](authorize-DRT.md)\. 

**Note**  
You can review AWS managed permissions policies by signing in to the IAM console and searching for the policies\.

You also can create your own custom IAM policies to allow permissions for AWS Shield API operations and resources\. You can attach these custom policies to the IAM users or groups that require those permissions or to custom execution roles \(IAM roles\) that you create for your Shield resources\. 

## Customer managed policy examples<a name="shd-access-policy-examples-for-sdk-cli"></a>

The examples in this section provide a group of sample policies that you can attach to a user\. If you are new to creating policies, we recommend that you first create an IAM user in your account and attach the policies to the user, in the sequence outlined in the steps in this section\.

You can use the console to verify the effects of each policy as you attach the policy to the user\. Initially, the user doesn't have permissions, and the user won't be able to do anything on the console\. As you attach policies to the user, you can verify that the user can perform various operations on the console\. 

We recommend that you use two browser windows: one to create the user and grant permissions, and the other to sign in to the AWS Management Console using the user's credentials and verify permissions as you grant them to the user\.

For examples that show how to create an IAM role that you can use as an execution role for your Shield resource, see [Creating IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create.html) in the *IAM User Guide*\.

### Example topics<a name="shd-topics4"></a>
+ [Example 1: Give users read\-only access to Shield, CloudFront, and CloudWatch](#shd-example1)
+ [Example 2: Give users full access to Shield, CloudFront, and CloudWatch](#shd-example2) 

### Create an IAM user<a name="shd-console-permissions-list-functions"></a>

First, you need to create an IAM user, add the user to an IAM group with administrative permissions, and then grant administrative permissions to the IAM user that you created\. You then can access AWS using a special URL and the user's credentials\. 

For instructions, see [Creating Your First IAM User and Administrators Group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html) in the *IAM User Guide*\. 

### Example 1: Give users read\-only access to Shield, CloudFront, and CloudWatch<a name="shd-example1"></a>

The following policy grants users read\-only access to Shield an associated resources, including Amazon CloudFront resources, and Amazon CloudWatch metrics\. It's useful for users who need permission to view the settings in Shield protections and attacks and to monitor metrics in CloudWatch\. These users can't create, update, or delete Shield resources\.

```
{
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "ProtectedResourcesReadAccess",
                "Effect": "Allow",
                "Action": [
                    "cloudfront:List*",
                    "elasticloadbalancing:List*",
                    "route53:List*",
                    "cloudfront:Describe*",
                    "elasticloadbalancing:Describe*",
                    "route53:Describe*",
                    "cloudwatch:Describe*",
                    "cloudwatch:Get*",
                    "cloudwatch:List*",
                    "cloudfront:GetDistribution*",
                    "globalaccelerator:ListAccelerators",
                    "globalaccelerator:DescribeAccelerator"
                ],
                "Resource": [
                    "arn:aws:elasticloadbalancing:*:*:*",
                    "arn:aws:cloudfront::*:*",
                    "arn:aws:route53:::hostedzone/*",
                    "arn:aws:cloudwatch:*:*:*:*",
                    "arn:aws:globalaccelerator::*:*"
                ]
            },
            {
                "Sid": "ShieldReadOnly",
                "Effect": "Allow",
                "Action": [
                    "shield:List*",
                    "shield:Describe*",
                    "shield:Get*"
                ],
                "Resource": "*"
            }
     ]
}
```

### Example 2: Give users full access to Shield, CloudFront, and CloudWatch<a name="shd-example2"></a>

The following policy lets users perform any Shield operation, perform any operation on CloudFront web distributions, and monitor metrics and a sample of requests in CloudWatch\. It's useful for users who are Shield administrators\.

```
{
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "ProtectedResourcesReadAccess",
                "Effect": "Allow",
                "Action": [
                    "cloudfront:List*",
                    "elasticloadbalancing:List*",
                    "route53:List*",
                    "cloudfront:Describe*",
                    "elasticloadbalancing:Describe*",
                    "route53:Describe*",
                    "cloudwatch:Describe*",
                    "cloudwatch:Get*",
                    "cloudwatch:List*",
                    "cloudfront:GetDistribution*",
                    "globalaccelerator:ListAccelerators",
                    "globalaccelerator:DescribeAccelerator"
                ],
                "Resource": [
                    "arn:aws:elasticloadbalancing:*:*:*",
                    "arn:aws:cloudfront::*:*",
                    "arn:aws:route53:::hostedzone/*",
                    "arn:aws:cloudwatch:*:*:*:*",
                    "arn:aws:globalaccelerator::*:*"
                ]
            },
            {
                "Sid": "ShieldFullAccess",
                "Effect": "Allow",
                "Action": [
                    "shield:*"
                ],
                "Resource": "*"
            }
      ]
}
```

We strongly recommend that you configure multi\-factor authentication \(MFA\) for users who have administrative permissions\. For more information, see [Using Multi\-Factor Authentication \(MFA\) Devices with AWS](https://docs.aws.amazon.com/IAM/latest/UserGuide/Using_ManagingMFA.html) in the *IAM User Guide*\. 