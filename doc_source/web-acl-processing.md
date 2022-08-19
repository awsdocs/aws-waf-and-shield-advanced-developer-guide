# Web ACL rule and rule group evaluation<a name="web-acl-processing"></a>

The way a web ACL handles a web request depends on the following: 
+ The numeric priority settings of the rules in the web ACL and inside rule groups
+ The action settings on the rules and web ACL
+ Any overrides that you place on the rules in the rule groups that you add

For a list of the rule action settings, see [AWS WAF rule action](waf-rule-action.md)\. 

You can customize request and response handling in your rule action settings and default web ACL action settings\. For information, see [Customized web requests and responses in AWS WAF](waf-custom-request-response.md)\.

**Topics**
+ [Processing order of rules and rule groups in a web ACL](web-acl-processing-order.md)
+ [Basic handling of the rule and rule group actions in a web ACL](web-acl-rule-actions.md)
+ [Overriding the actions of a rule group or its rules](web-acl-rule-group-override-options.md)