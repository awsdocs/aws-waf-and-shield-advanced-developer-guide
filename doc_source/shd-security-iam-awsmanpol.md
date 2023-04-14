# AWS managed policies for AWS Shield<a name="shd-security-iam-awsmanpol"></a>

To add permissions to users, groups, and roles, it is easier to use AWS managed policies than to write policies yourself\. It takes time and expertise to [create IAM customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create-console.html) that provide your team with only the permissions they need\. To get started quickly, you can use our AWS managed policies\. These policies cover common use cases and are available in your AWS account\. For more information about AWS managed policies, see [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

AWS services maintain and update AWS managed policies\. You can't change the permissions in AWS managed policies\. Services occasionally add additional permissions to an AWS managed policy to support new features\. This type of update affects all identities \(users, groups, and roles\) where the policy is attached\. Services are most likely to update an AWS managed policy when a new feature is launched or when new operations become available\. Services do not remove permissions from an AWS managed policy, so policy updates won't break your existing permissions\.

Additionally, AWS supports managed policies for job functions that span multiple services\. For example, the `ViewOnlyAccess` AWS managed policy provides read\-only access to many AWS services and resources\. When a service launches a new feature, AWS adds read\-only permissions for new operations and resources\. For a list and descriptions of job function policies, see [AWS managed policies for job functions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html) in the *IAM User Guide*\.

## AWS managed policy: AWSShieldDRTAccessPolicy<a name="shd-security-iam-awsmanpol-AWSShieldDRTAccessPolicy"></a>

AWS Shield uses this managed policy when you grant permission to the Shield Response Team \(SRT\) to act on your behalf\. This policy gives the SRT limited access to your AWS account, to assist with DDoS attack mitigation during high\-severity events\. This policy allows the SRT to manage your AWS WAF rules and Shield Advanced protections and to access your AWS WAF logs\. 

For information about granting permission to the SRT to operate on your behalf, see [Configuring access for the Shield Response Team \(SRT\)](ddos-srt-access.md)\.

For details about this policy, see [AWSShieldDRTAccessPolicy](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/service-role/AWSShieldDRTAccessPolicy) in the IAM console\.

## AWS managed policy: AWSShieldServiceRolePolicy<a name="shd-security-iam-awsmanpol-AWSShieldServiceRolePolicy"></a>

Shield Advanced uses this managed policy when you enable automatic application layer DDoS mitigation, to set the permissions it needs to manage resources for your account\. This policy allows Shield Advanced to create and apply AWS WAF rules and rule groups in the web ACLs that you've associated with your protected resources, to automatically respond to DDoS attacks\. 

You can't attach AWSShieldServiceRolePolicy to your IAM entities\. Shield attaches this policy to the service\-linked role `AWSServiceRoleForAWSShield` to allow Shield to perform actions on your behalf\. 

Shield Advanced enables the use of this policy when you enable automatic application layer DDoS mitigation\. For more information about the use for this policy, see [Shield Advanced automatic application layer DDoS mitigation](ddos-automatic-app-layer-response.md)\. 

For information about the service\-linked role AWSServiceRoleForAWSShield that uses this policy, see [Using service\-linked roles for Shield Advanced](shd-using-service-linked-roles.md)

For details about this policy, see [AWSShieldServiceRolePolicy](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/aws-service-role/AWSShieldServiceRolePolicy) in the IAM console\.

## Shield updates to AWS managed policies<a name="shd-security-iam-awsmanpol-updates"></a>



View details about updates to AWS managed policies for Shield since this service began tracking these changes\. For automatic alerts about changes to this page, subscribe to the RSS feed on the Shield document history page at [Document history](doc-history.md)\.




| Policy | Description of change | Date | 
| --- | --- | --- | 
|  `AWSShieldServiceRolePolicy` This policy allows Shield to access and manage AWS resources in order to automatically respond to application layer DDoS attacks on your behalf\.  Details in IAM console: [AWSShieldServiceRolePolicy](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/aws-service-role/AWSShieldServiceRolePolicy) The service\-linked role `AWSServiceRoleForAWSShield` uses this policy\. For information, see [Using service\-linked roles for Shield Advanced](shd-using-service-linked-roles.md)\.  |  Added this policy to provide Shield Advanced with the permissions required for the automatic application layer DDoS mitigation functionality\. For information about this feature, see [Shield Advanced automatic application layer DDoS mitigation](ddos-automatic-app-layer-response.md)\.  | December 1, 2021 | 
|  Shield started tracking changes  |  Shield started tracking changes for its AWS managed policies\.  | March 3, 2021 | 