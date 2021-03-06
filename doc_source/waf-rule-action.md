# AWS WAF rule action<a name="waf-rule-action"></a>

The rule action tells AWS WAF what to do with a web request when it matches the criteria defined in the rule\. You can optionally add custom behavior to each rule action\. 

Here are the rule action options: 
+ **Count** – AWS WAF counts the request but doesn't determine whether to allow it or block it\. With this action, AWS WAF continues processing the remaining rules in the web ACL\. You can insert custom headers into the request and you can add labels that other rules can match against\.
+ **Allow** – AWS WAF allows the request to be forwarded to the protected AWS resource for processing and response\. You can insert custom headers into the request before forwarding it to the protected resource\.
+ **Block** – AWS WAF blocks the request\. By default, the AWS resource responds with an HTTP `403 (Forbidden)` status code, but you can customize the response\. When AWS WAF blocks a request, the block action settings determine the response that the protected resource sends back to the client\. 

For information about customizing requests and responses, see [Customizing web requests and responses in AWS WAF](waf-custom-request-response.md)\.

For information about adding labels to matching requests, see [AWS WAF labels on web requests](waf-rule-labels.md)\.

You can override rule actions when you add them to a web ACL\. When you do this, the rule runs with the action set to count\. For more information about how web ACL and rule settings interact, see [Web ACL rule and rule group evaluation](web-acl-processing.md)\. 