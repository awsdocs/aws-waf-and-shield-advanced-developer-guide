# Adding a label to matching web requests<a name="waf-rule-label-add"></a>

When you define a label for a rule, AWS WAF adds the label to requests that match the rule\. You define a label in a rule by specifying the custom namespace strings and name to append to the label namespace prefix\. AWS WAF derives the prefix from the context in which you define the rule\. For information about this, see the label syntax information under [Label syntax and naming requirements](waf-rule-label-requirements.md)\. 

Except for the following, you can add labels to any rule and AWS WAF will add your labels to any web request that matches the rule match statement:
+ For rate\-based rules, labels are only added to web requests for a particular IP address while that IP address is blocked by AWS WAF due to rate limiting\. For information about rate\-based rules, see [Rate\-based rule statement](waf-rule-statement-type-rate-based.md)\. 
+ You can't use labels in statements that reference rule groups\. If you try to add a label to a rule group rule statement through the API, the operation throws a validation exception\. For information about these statement types, see [Managed rule group statement](waf-rule-statement-type-managed-rule-group.md) and [Rule group statement](waf-rule-statement-type-rule-group.md)\.

**WCUs ** – 1 WCU for every 5 labels that you define in your web ACL or rule group rules\.

**Where to find this**
+ **Rule builder** on the console – Under the rule's **Action** settings, under **Label**\. 
+ **API data type** – `Rule` `RuleLabels`