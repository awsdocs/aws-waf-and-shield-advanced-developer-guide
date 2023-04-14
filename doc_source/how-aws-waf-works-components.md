# AWS WAF components<a name="how-aws-waf-works-components"></a>

The following are the central components of AWS WAF:
+ **Web ACLs** – You use a web access control list \(ACL\) to protect a set of AWS resources\. You create a web ACL and define its protection strategy by adding rules\. Rules define criteria for inspecting web requests and they specify the action to take on requests that match their criteria\. You also set a default action for the web ACL that indicates whether to block or allow through any requests that the rules haven't already blocked or allowed\. 

  A web ACL is an AWS WAF resource\.
+ **Rules** – Each rule contains a statement that defines the inspection criteria, and an action to take if a web request meets the criteria\. When a web request meets the criteria, that's a match\. You can configure rules to block matching requests, allow them through, count them, or run bot controls against them that use CAPTCHA puzzles or silent client browser challenges\. 

  A rule is not an AWS WAF resource\. It only exists in the context of a web ACL or rule group\.
+ **Rule groups** – You can define rules directly inside a web ACL or in reusable rule groups\. AWS Managed Rules and AWS Marketplace sellers provide managed rule groups for your use\. You can also define your own rule groups\.

  A rule group is an AWS WAF resource\.