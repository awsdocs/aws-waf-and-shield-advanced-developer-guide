# Deciding on the default action for a web ACL<a name="web-acl-default-action"></a>

When you create and configure a web ACL, you must set the web ACL default action\. AWS WAF applies this action to any web request that makes it through all of the web ACL's rule evaluations without having a terminating action applied to it\. A terminating action stops the web ACL evaluation of the request and either lets it continue to your protected application or blocks it\. For information about rule actions, see [AWS WAF rule action](waf-rule-action.md)\.

The web ACL default action must determine the final disposition of the web request, so it's a terminating action: 
+ **Allow** – If you want to allow most users to access your website, but you want to block access to attackers whose requests originate from specified IP addresses, or whose requests appear to contain malicious SQL code or specified values, choose Allow for the default action\. Then, when you add rules to your web ACL, add rules that identify and block the specific requests that you want to block\. With this action, you can insert custom headers into the request before forwarding it to the protected resource\.
+ **Block** – If you want to prevent most users from accessing your website, but you want to allow access to users whose requests originate from specified IP addresses, or whose requests contain specified values, choose Block for the default action\. Then when you add rules to your web ACL, add rules that identify and allow the specific requests that you want to allow in\. By default, for the Block action, the AWS resource responds with an HTTP `403 (Forbidden)` status code, but you can customize the response\. 

For information about customizing requests and responses, see [Customized web requests and responses in AWS WAF](waf-custom-request-response.md)\.

Your configuration of your own rules and rule groups depends in part on whether you want to allow or block most web requests\. For example, if you want to *allow* most requests, you would set the web ACL default action to Allow, and then add rules that identify web requests that you want to *block*, such as the following:
+ Requests that originate from IP addresses that are making an unreasonable number of requests
+ Requests that originate from countries that either you don't do business in or are the frequent source of attacks
+ Requests that include fake values in the `User-agent` header
+ Requests that appear to include malicious SQL code

Managed rule group rules usually use the Block action, but not all do\. For examples, some rules used for Bot Control use the CAPTCHA and Challenge action settings\. For information about managed rule groups, see [Managed rule groups](waf-managed-rule-groups.md)\.