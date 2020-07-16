# AWS WAF rule action<a name="waf-rule-action"></a>

The rule action tells AWS WAF what to do with a web request when it matches the criteria defined in the rule\. 

Here are the rule action options: 
+ **Count** – AWS WAF counts the request but doesn't determine whether to allow it or block it\. With this action, AWS WAF continues processing the remaining rules in the web ACL\.
+ **Allow** – AWS WAF allows the request to be forwarded to the AWS resource for processing and response\. 
+ **Block** – AWS WAF blocks the request and the AWS resource responds with an HTTP 403 \(Forbidden\) status code\.

You can override rule actions when you add them to a web ACL\. When you do this, the rule runs with the action set to count\. For more information about how web ACL and rule settings interact, see [How AWS WAF processes a web ACL](web-acl-processing.md)\. 