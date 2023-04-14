# AWS Managed Rules for AWS WAF<a name="aws-managed-rule-groups"></a>

AWS Managed Rules for AWS WAF is a managed service that provides protection against common application vulnerabilities or other unwanted traffic\. You have the option of selecting one or more rule groups from AWS Managed Rules for each web ACL, up to the maximum web ACL capacity unit \(WCU\) limit\. 

**Mitigating false positives and testing rule group changes**  
Before using any managed rule group in production, test it in a non\-production environment according to the guidance at [Testing and tuning your AWS WAF protections](web-acl-testing.md)\. Follow the testing and tuning guidance when you add a rule group to your web ACL, to test a new version of a rule group, and whenever a rule group isn't handling your web traffic as you need it to\. 

**Shared security responsibilities**  
AWS Managed Rules are designed to protect you from common web threats\. When used in accordance with the documentation, AWS Managed Rules rule groups add another layer of security for your applications\. However, AWS Managed Rules rule groups aren't intended as a replacement for your security responsibilities, which are determined by the AWS resources that you select\. Refer to the [Shared Responsibility Model](https://aws.amazon.com/compliance/shared-responsibility-model/) to ensure that your resources in AWS are properly protected\. 