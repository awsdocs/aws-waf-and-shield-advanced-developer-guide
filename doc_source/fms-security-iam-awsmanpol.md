# AWS managed policies for AWS Firewall Manager<a name="fms-security-iam-awsmanpol"></a>





To add permissions to users, groups, and roles, it is easier to use AWS managed policies than to write policies yourself\. It takes time and expertise to [create IAM customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create-console.html) that provide your team with only the permissions they need\. To get started quickly, you can use our AWS managed policies\. These policies cover common use cases and are available in your AWS account\. For more information about AWS managed policies, see [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

AWS services maintain and update AWS managed policies\. You can't change the permissions in AWS managed policies\. Services occasionally add additional permissions to an AWS managed policy to support new features\. This type of update affects all identities \(users, groups, and roles\) where the policy is attached\. Services are most likely to update an AWS managed policy when a new feature is launched or when new operations become available\. Services do not remove permissions from an AWS managed policy, so policy updates won't break your existing permissions\.

Additionally, AWS supports managed policies for job functions that span multiple services\. For example, the `ViewOnlyAccess` AWS managed policy provides read\-only access to many AWS services and resources\. When a service launches a new feature, AWS adds read\-only permissions for new operations and resources\. For a list and descriptions of job function policies, see [AWS managed policies for job functions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html) in the *IAM User Guide*\.

## AWS managed policy: AWSFMAdminFullAccess<a name="security-iam-awsmanpol-AWSFMAdminFullAccess"></a>

Use the `AWSFMAdminFullAccess` AWS managed policy to allow your administrators to access AWS Firewall Manager resources, including all Firewall Manager policy types\. This policy doesn't include permissions for setting up Amazon Simple Notification Service notifications in AWS Firewall Manager\. For information about how to setting up access for Amazon Simple Notification Service, see [Setting up access for Amazon Simple Notification Service](https://docs.aws.amazon.com/sns/latest/dg/sns-setting-up.html)\.

**Permission details**

This policy is grouped into statements based on the set of permissions\.
+ **AWS Firewall Manager policy resources** \- Allows full administrative permissions to resources in AWS Firewall Manager, including all Firewall Manager policy types\.
+ **Write AWS WAF logs to Amazon Simple Storage Service** \- Allows Firewall Manager to write and read AWS WAF logs in Amazon S3\.
+ **Create service linked role** – Allows the administrator to create a service\-linked role, which allows Firewall Manager to access resources in other services on your behalf\. This permission allows creating the service\-linked role only for use by Firewall Manager\. For information about how Firewall Manager uses service linked roles, see [Using service\-linked roles for Firewall Manager](fms-using-service-linked-roles.md)\.
+ **AWS Organizations** – Allows administrators to use Firewall Manager for an organization in AWS Organizations\. After enabling trusted access for Firewall Manager in AWS Organizations, members of the admin account can view findings across their organization\. For information about using AWS Organizations with AWS Firewall Manager, see [Using AWS Organizations with other AWS services](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_integrate_services.html) in the *AWS Organizations User Guide*\.

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

This policy includes the following permissions:
+ `fms:*`:

  Lets you work with AWS Firewall Manager resources\.
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
+ `s3:GetBucketPolicy`:

  Lets you get the Amazon S3 bucket policy for AWS WAF logs\.
+ `ListDelegatedAdministrators`:

  Lets you list Amazon OpenSearch Service delegated administrators\.

## AWS managed policy: FMSServiceRolePolicy<a name="security-iam-awsmanpol-FMSServiceRolePolicy"></a>

This policy allows AWS Firewall Manager to manage AWS resources on your behalf in Firewall Manager and in integrated services\. This policy is attached to the service\-linked role `AWSServiceRoleForFMS`\. For more information about the service\-linked role, see [Using service\-linked roles for Firewall Manager](fms-using-service-linked-roles.md)\. 

For policy details, see the IAM console at [FMSServiceRolePolicy](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/aws-service-role/FMSServiceRolePolicy$serviceLevelSummary)\.

## AWS managed policy: AWSFMAdminReadOnlyAccess<a name="security-iam-awsmanpol-AWSFMAdminReadOnlyAccess"></a>

Grants read\-only access to all AWS Firewall Manager resources\.

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Action":[
            "fms:Get*",
            "fms:List*",
            "waf:Get*",
            "waf:List*",
            "waf-regional:Get*",
            "waf-regional:List*",
            "firehose:ListDeliveryStreams",
            "organizations:DescribeOrganization",
            "organizations:DescribeAccount",
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
            "s3:GetBucketPolicy"
         ],
         "Resource":[
            "arn:aws:s3:::aws-waf-logs-*"
         ]
      },
      {
         "Effect":"Allow",
         "Action":[
            "organizations:ListDelegatedAdministrators"
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

This policy includes the following permissions:
+ `fms:*`:

  Lets you view AWS Firewall Manager resources\.
+ `waf:Get*`, `waf-regional:Get*`:

  Lets you get AWS WAF policies\.
+ `waf:List*`, `waf-regional:List*`:

  Lets you list AWS WAF policies\.
+ `firehose:ListDeliveryStreams`:

  Lets you list AWS WAF logs\.
+ `organizations:DescribeOrganization`, `organizations:DescribeAccount`, `organizations:DescribeOrganization`, `organizations:ListRoots`, `organizations:ListChildren`, `organizations:ListAccounts`, `organizations:ListAccountsForParent`, `organizations:ListOrganizationalUnitsForParent`:

  Lets you view AWS Organizations resources\.
+ `shield:GetSubscriptionState`:

  Lets you get the subscription state for a AWS Shield policy\.
+ `route53resolver:ListFirewallRuleGroups`, `route53resolver:GetFirewallRuleGroup`:

  Lets you get and list Route 53 Private DNS for VPCs rule groups in an Route 53 Private DNS for VPCs policy\.
+ `wafv2:ListRuleGroups`, `wafv2:ListAvailableManagedRuleGroups`, `wafv2:CheckCapacity`, `wafv2:ListAvailableManagedRuleGroupVersions`:

  Lets you list AWS WAFV2 rule groups, AWS Managed Rules rule groups in AWS WAFV2 policies, AWS WAFV2 rule group capacity, and AWS WAFV2 AWS Managed Rules rule groups versions\.
+ `network-firewall:DescribeRuleGroup`, `network-firewall:DescribeRuleGroupMetadata`, `network-firewall:ListRuleGroups`:

  Lets you view AWS Network Firewall rule groups and rule group metadata\.
+ `ec2:DescribeAvailabilityZones`:

  Lets you view a AWS Network Firewall policy's Availability Zones\.
+ `ec2:DescribeRegions`:

  Lets you view a policy's Region in the AWS Firewall Manager console\.
+ `s3:GetBucketPolicy`:

  Lets you get the Amazon S3 bucket policy for AWS WAF logs\.
+ `ListDelegatedAdministrators`:

  Lets you list delegated administrators in AWS Organizations\.

## AWS managed policy: AWSFMMemberReadOnlyAccess<a name="security-iam-awsmanpol-AWSFMMemberReadOnlyAccess"></a>

Grants read\-only access to AWS Firewall Manager member resources\. For policy details, see the IAM console at [AWSFMMemberReadOnlyAccess](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/aws-service-role/AWSFMMemberReadOnlyAccess$serviceLevelSummary)\.













## Firewall Manager updates to AWS managed policies<a name="fms-security-iam-awsmanpol-updates"></a>

View details about updates to AWS managed policies for Firewall Manager since this service began tracking these changes\. For automatic alerts about changes to this page, subscribe to the RSS feed on the Firewall Manager document history page at [Document history](doc-history.md)\.




| Change | Description | Date | 
| --- | --- | --- | 
|  [FMSServiceRolePolicy](#security-iam-awsmanpol-FMSServiceRolePolicy) – Updated policy  |  Added permissions that allow Firewall Manager to describe Amazon EC2 instance and network interface attributes\. See the updated policy in the IAM console: [FMSServiceRolePolicy](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/FMSServiceRolePolicy$serviceLevelSummary)\.  | November 15, 2022 | 
|  [AWSFMAdminReadOnlyAccess](#security-iam-awsmanpol-AWSFMAdminReadOnlyAccess) – Updated policy  |  Added permissions to support AWS WAFV2, Shield, Network Firewall, DNS Firewall, Amazon VPC security group, policies\. See the updated policy in the IAM console: [AWSFMAdminReadOnlyAccess](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/AWSFMAdminReadOnlyAccess$serviceLevelSummary)\.  | November 02, 2022 | 
|  [AWSFMAdminFullAccess](#security-iam-awsmanpol-AWSFMAdminFullAccess) – Updated policy  |  Added permissions to support AWS WAFV2, Shield, Network Firewall, DNS Firewall, Amazon VPC security group, policies\. Removed Amazon SNS permissions\. See the updated policy in the IAM console: [AWSFMAdminFullAccess](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/AWSFMAdminFullAccess$serviceLevelSummary)\.  | October 21, 2022 | 
|  `FMSServiceRolePolicy` – New permissions for AWS Firewall Manager third\-party firewall policies  |  This change allows Firewall Manager to create and delete the Amazon EC2 VPC endpoints associated with a third\-party firewall policy\.  | March 30, 2022 | 
|  `FMSServiceRolePolicy` – New permissions for AWS Network Firewall policies  |  Added new permissions to support deployment of firewalls for Network Firewall policies\. The new permissions allow the retrieval of information about Availability Zones for accounts that are in scope of a policy\.   | February 16, 2022 | 
|  `FMSServiceRolePolicy` – New permissions for AWS Shield policies  |  Added new permissions to retrieve tags for AWS WAF regional and AWS WAF global resources\. Added AWS WAF regional permissions to retrieve web ACLs using a resource ARN\. Added permissions to support Shield automatic application layer DDoS mitigation\.   | January 07, 2022 | 
|  `FMSServiceRolePolicy` – New permissions for AWS Shield policies  |  Added new permission to retrieve tags for Elastic Load Balancing resources\.   | November 18, 2021 | 
|  `FMSServiceRolePolicy` – New permissions for security group and AWS Network Firewall policies  |  Added new permissions to enable centralized logging for AWS Network Firewall policies\. Additionally, read\-only Amazon EC2 permissions were added to support changes to the Config service that impact how AWS Firewall Manager queries resources for security group policies\.  | September 29, 2021 | 
|  `FMSServiceRolePolicy` – ARN formats for AWS WAF resources  |  Updated the `FMSServiceRolePolicy` to standardize the ARN formats for AWS WAF resources\. The updated ARN formats are `arn:aws:waf:*:*:*` and `arn:aws:waf-regional:*:*:*`\.  | August 12, 2021 | 
|  `FMSServiceRolePolicy` – Additional regions in China  |  AWS Firewall Manager has enabled `FMSServiceRolePolicy` for the BJS and ZHY regions in China\.  | August 12, 2021 | 
|  `FMSServiceRolePolicy` – Update to the existing policy  |  Added new permissions to allow AWS Firewall Manager to manage Amazon Route 53 Resolver DNS Firewall\. This change allows Firewall Manager to configure Amazon Route 53 Resolver DNS Firewall associations\. This permits you to use Firewall Manager to provide DNS Firewall protections for your VPCs throughout your organization in AWS Organizations\.  | March 17, 2021 | 
|  Firewall Manager started tracking changes  |  Firewall Manager started tracking changes for its AWS managed policies\.  | March 02, 2021 | 