# Managed rule group statement<a name="waf-rule-statement-type-managed-rule-group"></a>

The managed rule group rule statement adds a reference in your web ACL rules list to a managed rule group\. You don't see this option under your rule statements on the console, but when you work with the JSON format of your web ACL, any managed rule groups that you've added show up under the web ACL rules as this type\.

A managed rule group is either an AWS Managed Rules rule group, which is free for AWS WAF customers, or a AWS Marketplace managed rule group, which you can subscribe to through AWS Marketplace\. For more information, see [Managed rule groups](waf-managed-rule-groups.md)\.

When you add a rule group to a web ACL, you can exclude individual rules in the group from running, and you can override the actions of all rules in the rule group, to count only\. For more information, see [How AWS WAF processes a web ACL](web-acl-processing.md)\.

**Not nestable** – You can't nest this statement type inside other statements, and you can't include it in a rule group\. You can include it directly in a web ACL\. 

**WCUs** – Set for the rule group at creation\.

**Where to find this**
+ **Console** – During the process of creating a web ACL, on the **Add rules and rule groups** page, choose **Add managed rule groups**, and then find and select the rule group that you want to use\.
+ **API statement** – `ManagedRuleGroupStatement`