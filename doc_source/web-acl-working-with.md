# Working with Web ACLs<a name="web-acl-working-with"></a>

When you add rules to a web ACL, you specify whether you want AWS WAF to allow or block requests based on the conditions in the rules\. If you add more than one rule to a web ACL, AWS WAF evaluates each request against the rules in the order that you list them in the web ACL\. When a web request matches all the conditions in a rule, AWS WAF immediately takes the corresponding action—allow or block—and doesn't evaluate the request against the remaining rules in the web ACL, if any\. 

If a web request doesn't match any of the rules in a web ACL, AWS WAF takes the default action that you specified for the web ACL\. For more information, see [Deciding on the Default Action for a Web ACL](web-acl-default-action.md)\.

If you want to test a rule before you start using it to allow or block requests, you can configure AWS WAF to count the web requests that match the conditions in the rule\. For more information, see [Testing Web ACLs](web-acl-testing.md)\.


+ [Deciding on the Default Action for a Web ACL](web-acl-default-action.md)
+ [Creating a Web ACL](web-acl-creating.md)
+ [Associating or Disassociating a Web ACL with a CloudFront Distribution or an Application Load Balancer](web-acl-associating-cloudfront-distribution.md)
+ [Editing a Web ACL](web-acl-editing.md)
+ [Deleting a Web ACL](web-acl-deleting.md)
+ [Testing Web ACLs](web-acl-testing.md)