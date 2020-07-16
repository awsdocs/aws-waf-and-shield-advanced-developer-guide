# Rule group statement<a name="waf-rule-statement-type-rule-group"></a>

The rule group rule statement adds a reference to your web ACL rules list to a rule group that you manage\. You don't see this option under your rule statements on the console, but when you work with the JSON format of your web ACL, any of your own rule groups that you've added show up under the web ACL rules as this type\. For information about using your own rule groups, see [Managing your own rule groups](waf-user-created-rule-groups.md)\.

When you add a rule group to a web ACL, you can exclude individual rules in the group from running, and you can override the actions of all rules in the rule group, to count only\. For more information, see [How AWS WAF processes a web ACL](web-acl-processing.md)\.

**Not nestable** – You can't nest this statement type inside other statements, and you can't include it in a rule group\. You can include it directly in a web ACL\. 

**WCUs** – Set for the rule group at creation\.

**Where to find this**
+ **Console** – During the process of creating a web ACL, on the **Add rules and rule groups** page, choose **Add my own rules and rule groups**, **Rule group**, and then add the rule group that you want to use\.
+ **API statement** – `RuleGroupReferenceStatement`