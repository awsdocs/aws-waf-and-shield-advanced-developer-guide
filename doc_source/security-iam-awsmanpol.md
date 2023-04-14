# AWS managed policies for AWS WAF<a name="security-iam-awsmanpol"></a>

To add permissions to users, groups, and roles, it is easier to use AWS managed policies than to write policies yourself\. It takes time and expertise to [create IAM customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create-console.html) that provide your team with only the permissions they need\. To get started quickly, you can use our AWS managed policies\. These policies cover common use cases and are available in your AWS account\. For more information about AWS managed policies, see [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

AWS services maintain and update AWS managed policies\. You can't change the permissions in AWS managed policies\. Services occasionally add additional permissions to an AWS managed policy to support new features\. This type of update affects all identities \(users, groups, and roles\) where the policy is attached\. Services are most likely to update an AWS managed policy when a new feature is launched or when new operations become available\. Services do not remove permissions from an AWS managed policy, so policy updates won't break your existing permissions\.

Additionally, AWS supports managed policies for job functions that span multiple services\. For example, the `ViewOnlyAccess` AWS managed policy provides read\-only access to many AWS services and resources\. When a service launches a new feature, AWS adds read\-only permissions for new operations and resources\. For a list and descriptions of job function policies, see [AWS managed policies for job functions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html) in the *IAM User Guide*\.

## AWS managed policy: AWSWAFReadOnlyAccess<a name="security-iam-awsmanpol-AWSWAFReadOnlyAccess"></a>

This policy grants read\-only permissions that allow users to access AWS WAF resources but not modify them\. You can attach this policy to your IAM identities\. AWS WAF also attaches this policy to a service role that allows AWS WAF to perform actions on your behalf\.

For details about this policy, see [AWSWAFReadOnlyAccess](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/AWSWAFReadOnlyAccess$serviceLevelSummary) in the IAM console\.

## AWS managed policy: AWSWAFFullAccess<a name="security-iam-awsmanpol-AWSWAFFullAccess"></a>

This policy grants full access to AWS WAF resources\. You can attach this policy to your IAM identities\. AWS WAF also attaches this policy to a service role that allows AWS WAF to perform actions on your behalf\.

For details about this policy, see [AWSWAFFullAccess](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/AWSWAFFullAccess$serviceLevelSummary) in the IAM console\.

## AWS managed policy: AWSWAFConsoleReadOnlyAccess<a name="security-iam-awsmanpol-AWSWAFConsoleReadOnlyAccess"></a>

This policy grants read\-only permissions to the AWS WAF console, which includes resources for AWS WAF and for integrated services, such as Amazon CloudFront, Amazon API Gateway, Application Load Balancer, AWS AppSync, Amazon Cognito, and AWS App Runner\. You can attach this policy to your IAM identities\. AWS WAF also attaches this policy to a service role that allows AWS WAF to perform actions on your behalf\.

For details about this policy, see [AWSWAFConsoleReadOnlyAccess](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/AWSWAFConsoleReadOnlyAccess$serviceLevelSummary) in the IAM console\.

## AWS managed policy: AWSWAFConsoleFullAccess<a name="security-iam-awsmanpol-AWSWAFConsoleFullAccess"></a>

This policy grants full access to the AWS WAF console, which includes resources for AWS WAF and for integrated services, such as Amazon CloudFront, Amazon API Gateway, Application Load Balancer, AWS AppSync, Amazon Cognito, and AWS App Runner\. You can attach this policy to your IAM identities\. AWS WAF also attaches this policy to a service role that allows AWS WAF to perform actions on your behalf\.

For details about this policy, see [AWSWAFConsoleFullAccess](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/AWSWAFConsoleFullAccess$serviceLevelSummary) in the IAM console\.



## AWS WAF updates to AWS managed policies<a name="security-iam-awsmanpol-updates"></a>



View details about updates to AWS managed policies for AWS WAF since this service began tracking these changes\. For automatic alerts about changes to this page, subscribe to the RSS feed on the AWS WAF document history page at [Document history](doc-history.md)\.




| Policy | Description of change | Date | 
| --- | --- | --- | 
| `AWSWAFFullAccess` This policy allows AWS WAF to manage AWS resources on your behalf in AWS WAF and in integrated services\. Details in IAM console: [AWSWAFFullAccess](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/AWSWAFFullAccess$serviceLevelSummary)\. |  Expanded permissions to add AWS App Runner services to the resource types that you can protect with AWS WAF\.  | 2023\-03\-30 | 
| `AWSWAFReadOnlyAccess` This policy allows AWS WAF to manage AWS resources on your behalf in AWS WAF and in integrated services\. Details in IAM console: [AWSWAFReadOnlyAccess](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/AWSWAFReadOnlyAccess$serviceLevelSummary)\.  |  Expanded permissions to add AWS App Runner services to the resource types that you can protect with AWS WAF\.  | 2023\-03\-30 | 
|  `AWSWAFConsoleFullAccess` This policy allows AWS WAF to manage AWS console resources and other AWS resources on your behalf in AWS WAF and in integrated services\. Details in IAM console: [AWSWAFConsoleFullAccess](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/AWSWAFConsoleFullAccess$serviceLevelSummary)\.  |  Expanded permissions to add AWS App Runner services to the resource types that you can protect with AWS WAF\.  | 2023\-03\-30 | 
|  `AWSWAFConsoleReadOnlyAccess` This policy allows AWS WAF to manage AWS console resources and other AWS resources on your behalf in AWS WAF and in integrated services\. Details in IAM console: [AWSWAFConsoleReadOnlyAccess](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/AWSWAFConsoleReadOnlyAccess$serviceLevelSummary)\.  |  Expanded permissions to add AWS App Runner services to the resource types that you can protect with AWS WAF\.  | 2023\-03\-30 | 
| `AWSWAFFullAccess` This policy allows AWS WAF to manage AWS resources on your behalf in AWS WAF and in integrated services\. Details in IAM console: [AWSWAFFullAccess](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/AWSWAFFullAccess$serviceLevelSummary)\. |  Expanded permissions to add Amazon Cognito user pools to the resource types that you can protect with AWS WAF\.  | 2022\-08\-25 | 
| `AWSWAFReadOnlyAccess` This policy allows AWS WAF to manage AWS resources on your behalf in AWS WAF and in integrated services\. Details in IAM console: [AWSWAFReadOnlyAccess](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/AWSWAFReadOnlyAccess$serviceLevelSummary)\.  |  Expanded permissions to add Amazon Cognito user pools to the resource types that you can protect with AWS WAF\.  | 2022\-08\-25 | 
|  `AWSWAFConsoleFullAccess` This policy allows AWS WAF to manage AWS console resources and other AWS resources on your behalf in AWS WAF and in integrated services\. Details in IAM console: [AWSWAFConsoleFullAccess](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/AWSWAFConsoleFullAccess$serviceLevelSummary)\.  |  Expanded permissions to add Amazon Cognito user pools to the resource types that you can protect with AWS WAF\.  | 2022\-08\-25 | 
|  `AWSWAFConsoleReadOnlyAccess` This policy allows AWS WAF to manage AWS console resources and other AWS resources on your behalf in AWS WAF and in integrated services\. Details in IAM console: [AWSWAFConsoleReadOnlyAccess](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/AWSWAFConsoleReadOnlyAccess$serviceLevelSummary)\.  |  Expanded permissions to add Amazon Cognito user pools to the resource types that you can protect with AWS WAF\.  | 2022\-08\-25 | 
| `AWSWAFFullAccess` This policy allows AWS WAF to manage AWS resources on your behalf in AWS WAF and in integrated services\. Details in IAM console: [AWSWAFFullAccess](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/AWSWAFFullAccess$serviceLevelSummary)\.  |  Corrected the permissions settings for log delivery for Amazon Simple Storage Service \(Amazon S3\) and Amazon CloudWatch Logs\. This change resolves access denied errors that were occurring during logging configuration\. For information about logging your web ACL traffic, see [Logging web ACL traffic](logging.md)\.  | 2022\-01\-11 | 
|  `AWSWAFConsoleFullAccess` This policy allows AWS WAF to manage AWS console resources and other AWS resources on your behalf in AWS WAF and in integrated services\. Details in IAM console: [AWSWAFConsoleFullAccess](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/AWSWAFConsoleFullAccess$serviceLevelSummary)\.  |  Corrected the permissions settings for log delivery for Amazon Simple Storage Service \(Amazon S3\) and Amazon CloudWatch Logs\. This change resolves access errors that were occurring during logging configuration\. For information about logging your web ACL traffic, see [Logging web ACL traffic](logging.md)\.  | 2022\-01\-11 | 
|  `AWSWAFFullAccess` This policy allows AWS WAF to manage AWS resources on your behalf in AWS WAF and in integrated services\. Details in IAM console: [AWSWAFFullAccess](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/AWSWAFFullAccess$serviceLevelSummary)\.  |  Added new permissions for expanded logging options\. This change gives AWS WAF access to the additional logging destinations Amazon Simple Storage Service \(Amazon S3\) and Amazon CloudWatch Logs\. For information about logging your web ACL traffic, see [Logging web ACL traffic](logging.md)\.  | 2021\-11\-15 | 
|  `AWSWAFConsoleFullAccess` This policy allows AWS WAF to manage AWS console resources and other AWS resources on your behalf in AWS WAF and in integrated services\. Details in IAM console: [AWSWAFConsoleFullAccess](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/AWSWAFConsoleFullAccess$serviceLevelSummary)\.  |  Added new permissions for expanded logging options\. This change gives AWS WAF access to the additional logging destinations Amazon Simple Storage Service \(Amazon S3\) and Amazon CloudWatch Logs\. For information about logging your web ACL traffic, see [Logging web ACL traffic](logging.md)\.  | 2021\-11\-15 | 
|  AWS WAF started tracking changes  |  AWS WAF started tracking changes for its AWS managed policies\.  | 2021\-3\-01 | 