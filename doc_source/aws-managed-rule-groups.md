# AWS Managed Rules for AWS WAF<a name="aws-managed-rule-groups"></a>

AWS Managed Rules for AWS WAF is a managed service that provides protection against common application vulnerabilities or other unwanted traffic, without having to write your own rules\. You have the option of selecting one or more rule groups from AWS Managed Rules for each web ACL, up to the allowed maximum web ACL capacity unit \(WCU\) limit\. You can choose whether to count \(monitor\) or block requests that are matched by the managed rules\.

**Mitigating false positives and testing rule group changes**  
As a best practice, before using a rule group in production, test it in a non\-production environment according to the guidance at [Testing and tuning your AWS WAF protections](web-acl-testing.md)\. Follow the testing and tuning guidance when you add a rule group to your web ACL, to test a new version of a rule group, and whenever a rule group isn't handling your web traffic as you need it to\. 