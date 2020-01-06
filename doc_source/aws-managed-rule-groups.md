# AWS Managed Rules for AWS WAF<a name="aws-managed-rule-groups"></a>

AWS Managed Rules for AWS WAF is a managed service that provides protection against common application vulnerabilities or other unwanted traffic, without having to write your own rules\. You have the option of selecting one or more rule groups from AWS Managed Rules for each web ACL, up to the allowed maximum web ACL capacity unit \(WCU\) limit\. You can choose whether to count \(monitor\) or block requests that are matched by the managed rules\.

As a best practice, before using a rule group in production, test it in a non\-production environment, with the action override set to count\. Evaluate the rule group using Amazon CloudWatch metrics combined with AWS WAF sampled requests or AWS WAF logs\. When you're satisfied that the rule group does what you want, remove the override on the group\. 

**Mitigating False Positive Scenarios**  
If you are encountering false\-positive scenarios with AWS Managed Rules rule groups, perform the following steps: 

1. In the web ACL configuration, override the actions in the rules of the rule groups, putting them into count \(alert\) mode\. This stops them from blocking legitimate traffic\. 

1. Use either AWS WAF sampled requests or AWS WAF logs to identify which AWS Managed Rules rule group is triggering the false positive\. You can identify the AWS Managed Rules rule group by looking at the `ruleGroupId` field in the log or the `RuleWithinRuleGroup` in the sampled request\. The rule name follows this pattern: `AWS#<AMR RuleGroup Name>#<AMR Rule Name>`\. 

1. On the AWS WAF console, edit the web ACL, locate the AWS Managed Rules rule group that you've identified, and disable the rule that is causing the false positive\. 

For more information about a rule in an AWS Managed Rules rule group, contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\. 