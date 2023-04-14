# Managed rule group statement<a name="waf-rule-statement-type-managed-rule-group"></a>

The managed rule group rule statement adds a reference in your web ACL rules list to a managed rule group\. You don't see this option under your rule statements on the console, but when you work with the JSON format of your web ACL, any managed rule groups that you've added show up under the web ACL rules as this type\.

A managed rule group is either an AWS Managed Rules rule group, most of which are free for AWS WAF customers, or a AWS Marketplace managed rule group\. You automatically subscribe to the paid AWS Managed Rules rule groups when you add them to your web ACL\. You can subscribe to AWS Marketplace managed rule groups through AWS Marketplace\. For more information, see [Managed rule groups](waf-managed-rule-groups.md)\.

When you add a rule group to a web ACL, you can override the actions of rules in the group to Count or to another rule action\. For more information, see [Action overrides in rule groups](web-acl-rule-group-override-options.md)\.

You can narrow the scope of the requests that AWS WAF evaluates with the rule group\. To do this, you add a scope\-down statement inside the rule group statement\. For information about scope\-down statements, see [Scope\-down statements](waf-rule-scope-down-statements.md)\. This can help you manage how the rule group affects your traffic and can help you contain costs associated with traffic volume when you use the rule group\. For information and examples for using scope\-down statements with the AWS WAF Bot Control managed rule group, see [AWS WAF Bot Control](waf-bot-control.md)\.

**Not nestable** – You can't nest this statement type inside other statements, and you can't include it in a rule group\. You can include it directly in a web ACL\. 

**\(Optional\) Scope\-down statement** – This rule type takes an optional scope\-down statement, to narrow the scope of the requests that the rule group evaluates\. For more information, see [Scope\-down statements](waf-rule-scope-down-statements.md)\.

**WCUs** – Set for the rule group at creation\.

**Where to find this rule statement**
+ **Console** – During the process of creating a web ACL, on the **Add rules and rule groups** page, choose **Add managed rule groups**, and then find and select the rule group that you want to use\.
+ **API** – [ManagedRuleGroupStatement](https://docs.aws.amazon.com/waf/latest/APIReference/API_ManagedRuleGroupStatement.html)