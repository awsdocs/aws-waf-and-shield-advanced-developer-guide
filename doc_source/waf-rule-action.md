# AWS WAF rule action<a name="waf-rule-action"></a>

The rule action tells AWS WAF what to do with a web request when it matches the criteria defined in the rule\. You can optionally add custom behavior to each rule action\. 

Here are the rule action options: 
+ **Count** – AWS WAF counts the request but doesn't determine whether to allow it or block it\. With this action, AWS WAF continues processing the remaining rules in the web ACL\. You can insert custom headers into the request and you can add labels that other rules can match against\.
+ **Allow** – AWS WAF allows the request to be forwarded to the protected AWS resource for processing and response\. This action terminates the web ACL evaluation of the request\. You can insert custom headers into the request before forwarding it to the protected resource\.
+ **Block** – AWS WAF blocks the request\. This action terminates the web ACL evaluation of the request\. By default, the AWS resource responds with an HTTP `403 (Forbidden)` status code, but you can customize the response\. When AWS WAF blocks a request, the block action settings determine the response that the protected resource sends back to the client\. 
+ **CAPTCHA** – AWS WAF runs a CAPTCHA check against the request\. The action that AWS WAF takes on the request can be terminating or non\-terminating, depending on the results of the check: 
  + If the request includes a valid, unexpired CAPTCHA token, AWS WAF handles it similar to the **Count** action handling\. AWS WAF continues to inspect the web request based on the remaining rules in the web ACL\. You can optionally configure custom headers to insert into the request and you can add labels that other rules can match against\. 
  + If the request doesn't include a valid CAPTCHA token, AWS WAF terminates the inspection of the web request and blocks the request, similar to the **Block** action\. AWS WAF then responds to the client with an error, and includes a CAPTCHA challenge if the request indicates that the client can handle it\. 

  For additional information about CAPTCHA, see [AWS WAF CAPTCHA](waf-captcha.md)\.

For more information about customizing requests and responses, see [Customized web requests and responses in AWS WAF](waf-custom-request-response.md)\.

For information about adding labels to matching requests, see [Labels on web requests](waf-labels.md)\.

For information about how web ACL and rule settings interact, see [Web ACL rule and rule group evaluation](web-acl-processing.md)\. 