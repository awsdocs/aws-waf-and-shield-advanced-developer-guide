# Managing and using a web access control list \(web ACL\)<a name="web-acl"></a>

A web access control list \(web ACL\) gives you fine\-grained control over all of the HTTP\(S\) web requests that your protected resource responds to\. You can protect Amazon CloudFront, Amazon API Gateway, Application Load Balancer, and AWS AppSync resources\. 

You can use criteria like the following to allow or block requests: 
+ IP address origin of the request
+ Country of origin of the request
+ String match or regular expression \(regex\) match in a part of the request
+ Size of a particular part of the request
+ Detection of malicious SQL code or scripting 

You can also test for any combination of these conditions\. You can block or count web requests that not only meet the specified conditions, but also exceed a specified number of requests in any 5\-minute period\. You can combine conditions using logical operators\. 

This criteria is provided inside the rules that you include in your web ACL and in rule groups that you use in the web ACL\. It's specified in the rule statement\. For a full list of the options, see [AWS WAF rule statements](waf-rule-statements.md)\.

To choose the requests that you want to allow to have access to your content or that you want to block, perform the following tasks:

1. Choose the default action, either allow or block, for web requests that don't match any of the rules that you specify\. For more information, see [Deciding on the default action for a web ACL](web-acl-default-action.md)\.

1. Add any rule groups that you want to use in your web ACL\. Managed rule groups usually contain rules that block web requests\. For information about rule groups, see [Rule groups](waf-rule-groups.md)\. 

1. Specify additional conditions under which you want to allow or block requests in one or more rules\. To add more than one, start with `AND` or `OR` rule statements and nest the rules that you want to combine under those\. If you want to negate a rule option, nest the rule in a NOT statement\. You can optionally use a rate\-based rule instead of a regular rule to limit the number of requests from any single IP address that meets the conditions\. For information about rules, see [AWS WAF rules](waf-rules.md)\.

If you add more than one rule to a web ACL, AWS WAF evaluates the rules in the order that they're listed for the web ACL\. For more information, see [Web ACL rule and rule group evaluation](web-acl-processing.md)\.

When you create a web ACL, you specify the types of resources that you want to use it with\. For information, see [Creating a web ACL](web-acl-creating.md)\. After you define a web ACL, you can associate it with your resources to begin providing protection for them\. For more information, see [Associating or disassociating a web ACL with an AWS resource](web-acl-associating-aws-resource.md)\. 

## How AWS resources handle response delays from AWS WAF<a name="web-acl-processing-resource-default"></a>

On some occasions, AWS WAF might encounter an internal error that delays the response to associated AWS resources about whether to allow or block a request\. On those occasions, CloudFront typically allows the request or serves the content, while the Regional services typically deny the request and don't serve the content\.

**Topics**
+ [How AWS resources handle response delays from AWS WAF](#web-acl-processing-resource-default)
+ [Web ACL rule and rule group evaluation](web-acl-processing.md)
+ [Deciding on the default action for a web ACL](web-acl-default-action.md)
+ [Working with web ACLs](web-acl-working-with.md)