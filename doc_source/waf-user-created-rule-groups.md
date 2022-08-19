# Managing your own rule groups<a name="waf-user-created-rule-groups"></a>

You can create your own rule group to reuse collections of rules that you either don't find in the managed rule group offerings or that you prefer to handle on your own\. 

Rule groups that you create hold rules just like a web ACL does, and you add rules to a rule group in the same way as you do to a web ACL\. When you create your own rule group, you must set an immutable maximum capacity for it\. 

You can share a rule group that you own with another AWS account, for use by that account\. This option is available through the AWS WAF API\. For more information, see [PutPermissionPolicy](https://docs.aws.amazon.com/waf/latest/APIReference/API_PutPermissionPolicy.html) in the AWS WAF API Reference\.

**Topics**
+ [Creating a rule group](waf-rule-group-creating.md)
+ [Using your rule group in a web ACL](waf-rule-group-using.md)
+ [Deleting a rule group](waf-rule-group-deleting.md)