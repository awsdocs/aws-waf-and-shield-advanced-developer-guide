# Deciding on the default action for a web ACL<a name="web-acl-default-action"></a>

When you create and configure a web ACL, you set the web ACL default action, which determines how AWS WAF handles web requests that don't match any rules in the web ACL\. The default action must be a terminating action: 
+ **Allow** – If you want to allow most users to access your website, but you want to block access to attackers whose requests originate from specified IP addresses, or whose requests appear to contain malicious SQL code or specified values, choose allow for the default action\. Then, when you add rules to your web ACL, add rules that identify and block the specific requests that you want to block\. With this action, you can insert custom headers into the request before forwarding it to the protected resource\.
+ **Block** – If you want to prevent most users from accessing your website, but you want to allow access to users whose requests originate from specified IP addresses, or whose requests contain specified values, choose block for the default action\. Then when you add rules to your web ACL, add rules that identify and allow the specific requests that you want to allow in\. By default, for the block action, the AWS resource responds with an HTTP `403 (Forbidden)` status code, but you can customize the response\. 

For information about customizing requests and responses, see [Customized web requests and responses in AWS WAF](waf-custom-request-response.md)\.

Your configuration of your own rules and rule groups depends in part on whether you want to allow or block most web requests\. For example, if you want to *allow* most requests, you would set the web ACL default action to allow, and then add rules that identify web requests that you want to *block*, such as the following:
+ Requests that originate from IP addresses that are making an unreasonable number of requests
+ Requests that originate from countries that either you don't do business in or are the frequent source of attacks
+ Requests that include fake values in the `User-agent` header
+ Requests that appear to include malicious SQL code

Managed rule groups usually use the block action\. For information about managed rule groups, see [Managed rule groups](waf-managed-rule-groups.md)\.