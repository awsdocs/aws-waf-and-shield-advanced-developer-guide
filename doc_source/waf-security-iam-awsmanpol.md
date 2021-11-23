# AWS managed policies for AWS WAF<a name="waf-security-iam-awsmanpol"></a>





To add permissions to users, groups, and roles, it is easier to use AWS managed policies than to write policies yourself\. It takes time and expertise to [create IAM customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create-console.html) that provide your team with only the permissions they need\. To get started quickly, you can use our AWS managed policies\. These policies cover common use cases and are available in your AWS account\. For more information about AWS managed policies, see [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

AWS services maintain and update AWS managed policies\. You can't change the permissions in AWS managed policies\. Services occasionally add additional permissions to an AWS managed policy to support new features\. This type of update affects all identities \(users, groups, and roles\) where the policy is attached\. Services are most likely to update an AWS managed policy when a new feature is launched or when new operations become available\. Services do not remove permissions from an AWS managed policy, so policy updates won't break your existing permissions\.

Additionally, AWS supports managed policies for job functions that span multiple services\. For example, the **ViewOnlyAccess** AWS managed policy provides read\-only access to many AWS services and resources\. When a service launches a new feature, AWS adds read\-only permissions for new operations and resources\. For a list and descriptions of job function policies, see [AWS managed policies for job functions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html) in the *IAM User Guide*\.













## AWS WAF updates to AWS managed policies<a name="waf-security-iam-awsmanpol-updates"></a>



View details about updates to AWS managed policies for AWS WAF since this service began tracking these changes\. For automatic alerts about changes to this page, subscribe to the RSS feed on the AWS WAF document history page at [Document history](doc-history.md)\.




| Policy | Description of change | Date | 
| --- | --- | --- | 
| `AWSWAFFullAccess` This policy allows AWS WAF to manage AWS resources on your behalf in AWS WAF and in integrated services\. Details in IAM console: [AWSWAFFullAccess](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/AWSWAFFullAccess$serviceLevelSummary) |  Added new permissions for expanded logging options\. This change gives AWS WAF access to the additional logging destinations Amazon Simple Storage Service \(Amazon S3\) and Amazon CloudWatch Logs\. For information about logging your web ACL traffic, see [Logging and monitoring web ACL traffic](logging.md)\.  | November 15, 2021 | 
|  `AWSWAFConsoleFullAccess` This policy allows AWS WAF to manage AWS console resources and other AWS resources on your behalf in AWS WAF and in integrated services\. Details in IAM console: [AWSWAFConsoleFullAccess](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/AWSWAFConsoleFullAccess$serviceLevelSummary)  |  Added new permissions for expanded logging options\. This change gives AWS WAF access to the additional logging destinations Amazon Simple Storage Service \(Amazon S3\) and Amazon CloudWatch Logs\. For information about logging your web ACL traffic, see [Logging and monitoring web ACL traffic](logging.md)\.  | November 15, 2021 | 
|  AWS WAF started tracking changes  |  AWS WAF started tracking changes for its AWS managed policies\.  | March 1, 2021 | 