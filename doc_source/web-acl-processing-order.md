# Processing order of rules and rule groups in a web ACL<a name="web-acl-processing-order"></a>

If you add more than one rule or rule group to a web ACL, AWS WAF evaluates each web request against them in the order that you list them in the web ACL\. In each rule group, AWS WAF processes the rules in the order in which they're listed in the rule group\. 

For example, say you have the following rules and rule groups in your web ACL, ordered as shown:
+ Rule1
+ RuleGroupA
  + RuleA1
  + RuleA2
+ Rule2
+ RuleGroupB
  + RuleB1
  + RuleB2

AWS WAF would evaluate the rules for this web ACL in the following order:
+ Rule1
+ RuleGroupA RuleA1
+ RuleGroupA RuleA2
+ Rule2
+ RuleGroupB RuleB1
+ RuleGroupB RuleB2