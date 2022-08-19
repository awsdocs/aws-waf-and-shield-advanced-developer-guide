# Processing order of rules and rule groups in a web ACL<a name="web-acl-processing-order"></a>

In a web ACL and inside any rule group, you determine the evaluation order of the rules using numeric priority settings\. You must give each rule in a web ACL a unique priority setting within that web ACL, and you must give each rule in a rule group a unique priority setting within that rule group\. 

**Note**  
When you manage rule groups and web ACLs through the console, AWS WAF assigns unique numeric priority settings for you based on the order of the rules in the list\. AWS WAF assigns the lowest numeric priority to the rule at the top of the list, and the highest numeric priority to the rule at the bottom\. 

When AWS WAF evaluates any web ACL or rule group against a web request, it evaluates the rules from the lowest numeric priority setting on up until it either finds a match that terminates the evaluation or exhausts all of the rules\.

For example, say you have the following rules and rule groups in your web ACL, prioritized as shown:
+ Rule1 – priority 0
+ RuleGroupA – priority 100
  + RuleA1 – priority 10,000
  + RuleA2 – priority 20,000
+ Rule2 – priority 200
+ RuleGroupB – priority 300
  + RuleB1 – priority 0
  + RuleB2 – priority 1

AWS WAF would evaluate the rules for this web ACL in the following order:
+ Rule1
+ RuleGroupA RuleA1
+ RuleGroupA RuleA2
+ Rule2
+ RuleGroupB RuleB1
+ RuleGroupB RuleB2