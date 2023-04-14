# Identity\-based policy examples for AWS Firewall Manager<a name="fms-security_iam_id-based-policy-examples"></a>

By default, users and roles don't have permission to create or modify Firewall Manager resources\. They also can't perform tasks by using the AWS Management Console, AWS Command Line Interface \(AWS CLI\), or AWS API\. To grant users permission to perform actions on the resources that they need, an IAM administrator can create IAM policies\. The administrator can then add the IAM policies to roles, and users can assume the roles\.

To learn how to create an IAM identity\-based policy by using these example JSON policy documents, see [Creating IAM policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create-console.html) in the *IAM User Guide*\.

For details about actions and resource types defined by Firewall Manager, including the format of the ARNs for each of the resource types, see [Actions, resources, and condition keys for AWS Firewall Manager](https://docs.aws.amazon.com/service-authorization/latest/reference/list_awsfirewallmanager.html) in the *Service Authorization Reference*\.

**Topics**
+ [Policy best practices](#fms-security_iam_service-with-iam-policy-best-practices)
+ [Using the Firewall Manager console](#fms-security_iam_id-based-policy-examples-console)
+ [Allow users to view their own permissions](#fms-security_iam_id-based-policy-examples-view-own-permissions)
+ [Grant read access to your Firewall Manager security groups](#fms-example0)
+ [Granting full access to AWS Firewall Manager resources](#fms-access-manually-grant-full-access)

## Policy best practices<a name="fms-security_iam_service-with-iam-policy-best-practices"></a>

Identity\-based policies determine whether someone can create, access, or delete Firewall Manager resources in your account\. These actions can incur costs for your AWS account\. When you create or edit identity\-based policies, follow these guidelines and recommendations:
+ **Get started with AWS managed policies and move toward least\-privilege permissions** – To get started granting permissions to your users and workloads, use the *AWS managed policies* that grant permissions for many common use cases\. They are available in your AWS account\. We recommend that you reduce permissions further by defining AWS customer managed policies that are specific to your use cases\. For more information, see [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) or [AWS managed policies for job functions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html) in the *IAM User Guide*\.
+ **Apply least\-privilege permissions** – When you set permissions with IAM policies, grant only the permissions required to perform a task\. You do this by defining the actions that can be taken on specific resources under specific conditions, also known as *least\-privilege permissions*\. For more information about using IAM to apply permissions, see [ Policies and permissions in IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html) in the *IAM User Guide*\.
+ **Use conditions in IAM policies to further restrict access** – You can add a condition to your policies to limit access to actions and resources\. For example, you can write a policy condition to specify that all requests must be sent using SSL\. You can also use conditions to grant access to service actions if they are used through a specific AWS service, such as AWS CloudFormation\. For more information, see [ IAM JSON policy elements: Condition](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition.html) in the *IAM User Guide*\.
+ **Use IAM Access Analyzer to validate your IAM policies to ensure secure and functional permissions** – IAM Access Analyzer validates new and existing policies so that the policies adhere to the IAM policy language \(JSON\) and IAM best practices\. IAM Access Analyzer provides more than 100 policy checks and actionable recommendations to help you author secure and functional policies\. For more information, see [IAM Access Analyzer policy validation](https://docs.aws.amazon.com/IAM/latest/UserGuide/access-analyzer-policy-validation.html) in the *IAM User Guide*\.
+ **Require multi\-factor authentication \(MFA\)** – If you have a scenario that requires IAM users or a root user in your AWS account, turn on MFA for additional security\. To require MFA when API operations are called, add MFA conditions to your policies\. For more information, see [ Configuring MFA\-protected API access](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_configure-api-require.html) in the *IAM User Guide*\.

For more information about best practices in IAM, see [Security best practices in IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) in the *IAM User Guide*\.

## Using the Firewall Manager console<a name="fms-security_iam_id-based-policy-examples-console"></a>

To access the AWS Firewall Manager console, you must have a minimum set of permissions\. These permissions must allow you to list and view details about the Firewall Manager resources in your AWS account\. If you create an identity\-based policy that is more restrictive than the minimum required permissions, the console won't function as intended for entities \(users or roles\) with that policy\.

You don't need to allow minimum console permissions for users that are making calls only to the AWS CLI or the AWS API\. Instead, allow access to only the actions that match the API operation that they're trying to perform\.

To ensure that users and roles can still use the Firewall Manager console, also attach the Firewall Manager `ConsoleAccess` or `ReadOnly` AWS managed policy to the entities\. For more information, see [Adding permissions to a user](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_change-permissions.html#users_change_permissions-add-console) in the *IAM User Guide*\.

## Allow users to view their own permissions<a name="fms-security_iam_id-based-policy-examples-view-own-permissions"></a>

This example shows how you might create a policy that allows IAM users to view the inline and managed policies that are attached to their user identity\. This policy includes permissions to complete this action on the console or programmatically using the AWS CLI or AWS API\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "ViewOwnUserInfo",
            "Effect": "Allow",
            "Action": [
                "iam:GetUserPolicy",
                "iam:ListGroupsForUser",
                "iam:ListAttachedUserPolicies",
                "iam:ListUserPolicies",
                "iam:GetUser"
            ],
            "Resource": ["arn:aws:iam::*:user/${aws:username}"]
        },
        {
            "Sid": "NavigateInConsole",
            "Effect": "Allow",
            "Action": [
                "iam:GetGroupPolicy",
                "iam:GetPolicyVersion",
                "iam:GetPolicy",
                "iam:ListAttachedGroupPolicies",
                "iam:ListGroupPolicies",
                "iam:ListPolicyVersions",
                "iam:ListPolicies",
                "iam:ListUsers"
            ],
            "Resource": "*"
        }
    ]
}
```

## Grant read access to your Firewall Manager security groups<a name="fms-example0"></a>

Firewall Manager allows cross\-account resource access, but it doesn't allow you to create cross\-account resource protections\. You can only create protections for resources from within the account that owns those resources\. 

The following is an example policy that grants permissions for the `fms:Get`,`fms:List`, and `ec2:DescribeSecurityGroups` actions on all resources\. 

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

## Granting full access to AWS Firewall Manager resources<a name="fms-access-manually-grant-full-access"></a>

Follow this guidance if you have difficulty creating or managing your Firewall Manager policies with the managed policy, `AWSFMAdminFullAccess`\. For information about working with managed policies for AWS Firewall Manager, see \.

This policy doesn't include permissions for setting up Amazon Simple Notification Service notifications in AWS Firewall Manager\. For information about how to setting up access for Amazon Simple Notification Service, see [Setting up access for Amazon Simple Notification Service](https://docs.aws.amazon.com/sns/latest/dg/sns-setting-up.html)\.

Use the following policy to grant full administrative access to your account:

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Action":[
            "fms:*",
            "waf:*",
            "waf-regional:*",
            "elasticloadbalancing:SetWebACL",
            "firehose:ListDeliveryStreams",
            "organizations:DescribeAccount",
            "organizations:DescribeOrganization",
            "organizations:ListRoots",
            "organizations:ListChildren",
            "organizations:ListAccounts",
            "organizations:ListAccountsForParent",
            "organizations:ListOrganizationalUnitsForParent",
            "shield:GetSubscriptionState",
            "route53resolver:ListFirewallRuleGroups",
            "route53resolver:GetFirewallRuleGroup",
            "wafv2:ListRuleGroups",
            "wafv2:ListAvailableManagedRuleGroups",
            "wafv2:CheckCapacity",
            "wafv2:PutLoggingConfiguration",
            "wafv2:ListAvailableManagedRuleGroupVersions",
            "network-firewall:DescribeRuleGroup",
            "network-firewall:DescribeRuleGroupMetadata",
            "network-firewall:ListRuleGroups",
            "ec2:DescribeAvailabilityZones",
            "ec2:DescribeRegions"
         ],
         "Resource":"*"
      },
      {
         "Effect":"Allow",
         "Action":[
            "s3:PutBucketPolicy",
            "s3:GetBucketPolicy"
         ],
         "Resource":[
            "arn:aws:s3:::aws-waf-logs-*"
         ]
      },
      {
         "Effect":"Allow",
         "Action":"iam:CreateServiceLinkedRole",
         "Resource":"*",
         "Condition":{
            "StringEquals":{
               "iam:AWSServiceName":[
                  "fms.amazonaws.com"
               ]
            }
         }
      },
      {
         "Effect":"Allow",
         "Action":[
            "organizations:EnableAWSServiceAccess",
            "organizations:ListDelegatedAdministrators",
            "organizations:RegisterDelegatedAdministrator",
            "organizations:DeregisterDelegatedAdministrator"
         ],
         "Resource":"*",
         "Condition":{
            "StringEquals":{
               "organizations:ServicePrincipal":[
                  "fms.amazonaws.com"
               ]
            }
         }
      }
   ]
}
```

**Permission details**

This policy includes the following permissions\.:
+ `fms:*`:

  Lets you work with AWS Firewall Manager resources\.
+ `waf:*`, `waf-regional:*`:

  Lets you work with AWS WAF policies\.
+ `waf:*`, `waf-regional:*`:

  Lets you work with AWS WAF policies\.
+ `elasticloadbalancing:SetWebACL`:

  Lets you associate web access control lists \(ACLs\) to Elastic Load Balancers\.
+ `firehose:ListDeliveryStreams`:

  Lets you view AWS WAF logs\.
+ `organizations:DescribeAccount`, `organizations:DescribeOrganization`, `organizations:ListRoots`, `organizations:ListChildren`, `organizations:ListAccounts`, `organizations:ListAccountsForParent`, `organizations:ListOrganizationalUnitsForParent`:

  Lets you work with AWS Organizations\.
+ `shield:GetSubscriptionState`:

  Lets you view the subscription state for a AWS Shield policy\.
+ `route53resolver:ListFirewallRuleGroups`, `route53resolver:GetFirewallRuleGroup`:

  Lets you work with Route 53 Private DNS for VPCs rule groups in an Route 53 Private DNS for VPCs policy\.
+ `wafv2:ListRuleGroups`, `wafv2:ListAvailableManagedRuleGroups`, `wafv2:CheckCapacity`, `wafv2:PutLoggingConfiguration`, `wafv2:ListAvailableManagedRuleGroupVersions`:

  Lets you work with AWS WAFV2 policies\.
+ `network-firewall:DescribeRuleGroup`, `network-firewall:DescribeRuleGroupMetadata`, `network-firewall:ListRuleGroups`:

  Lets you work with AWS Network Firewall policies\.
+ `ec2:DescribeAvailabilityZones`:

  Lets you view a AWS Network Firewall policy's Availability Zones\.
+ `ec2:DescribeRegions`:

  Lets you view a policy's Region in the AWS Firewall Manager console\.