# AWS managed policies for AWS Shield Advanced<a name="shd-security-iam-awsmanpol"></a>





To add permissions to users, groups, and roles, it is easier to use AWS managed policies than to write policies yourself\. It takes time and expertise to [create IAM customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create-console.html) that provide your team with only the permissions they need\. To get started quickly, you can use our AWS managed policies\. These policies cover common use cases and are available in your AWS account\. For more information about AWS managed policies, see [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

AWS services maintain and update AWS managed policies\. You can't change the permissions in AWS managed policies\. Services occasionally add additional permissions to an AWS managed policy to support new features\. This type of update affects all identities \(users, groups, and roles\) where the policy is attached\. Services are most likely to update an AWS managed policy when a new feature is launched or when new operations become available\. Services do not remove permissions from an AWS managed policy, so policy updates won't break your existing permissions\.

Additionally, AWS supports managed policies for job functions that span multiple services\. For example, the `ViewOnlyAccess` AWS managed policy provides read\-only access to many AWS services and resources\. When a service launches a new feature, AWS adds read\-only permissions for new operations and resources\. For a list and descriptions of job function policies, see [AWS managed policies for job functions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html) in the *IAM User Guide*\.













## Shield Advanced updates to AWS managed policies<a name="shd-security-iam-awsmanpol-updates"></a>



View details about updates to AWS managed policies for Shield Advanced since this service began tracking these changes\. For automatic alerts about changes to this page, subscribe to the RSS feed on the Shield Advanced document history page at [Document history](doc-history.md)\.




| Policy | Description of change | Date | 
| --- | --- | --- | 
|  `AWSShieldServiceRolePolicy` This policy allows Shield Advanced to access and manage AWS resources in order to automatically respond to application layer DDoS attacks on your behalf\.  Details in IAM console: [AWSShieldServiceRolePolicy](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/aws-service-role/AWSShieldServiceRolePolicy$serviceLevelSummary) The service\-linked role `AWSServiceRoleForAWSShield` uses this policy\. For information, see [Using service\-linked roles for Shield Advanced](shd-using-service-linked-roles.md)\.  |  Added policy to provide Shield Advanced with the permissions required for the automatic application layer DDoS mitigation functionality\. For information about this feature, see [Shield Advanced automatic application layer DDoS mitigation](ddos-automatic-app-layer-response.md)\.  | December 1, 2021 | 
|  Shield Advanced started tracking changes  |  Shield Advanced started tracking changes for its AWS managed policies\.  | March 1, 2021 | 