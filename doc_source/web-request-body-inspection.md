# Web request body inspection<a name="web-request-body-inspection"></a>

AWS WAF doesn't support inspecting the entire contents of web requests whose bodies exceed 8 KB \(8,192 bytes\)\. Only the first 8 KB of the request body are forwarded to AWS WAF for inspection\. 

This can affect your AWS WAF web request inspection in the following situations:
+ When you write a rule for AWS WAF that inspects the request component **Body** or **JSON body**\. For information about specifying a request component in a rule, see [AWS WAF rules](waf-rules.md) and [Web request component settings](waf-rule-statement-fields.md)\.
+ When you use a managed rule group with a rule that inspects the request body\. For information about which AWS Managed Rules inspect the request body, see [AWS Managed Rules rule groups list](aws-managed-rule-groups-list.md)\. For information about which AWS Marketplace rules inspect the request body, ask your rule group provider\. 

If you don't need to inspect more than 8 KB of the body, you can prevent additional bytes from passing through with a size constraint rule statement\. Add the size constraint rule to your web ACL so that it runs before any statement that inspects the body, and configure the size constraint to block request bodies over 8 KB\. For information about size constraint statements, see [Size constraint rule statement](waf-rule-statement-type-size-constraint-match.md)\. 

**To block web request bodies over 8 KB before inspecting the body**

1. When you create or edit your web ACL, in the rules settings, choose **Add rules**, **Add my own rules and rule groups**, **Rule builder**, then **Rule visual editor**\. For guidance creating or editing a web ACL, see [Working with web ACLs](web-acl-working-with.md)\.

1. Enter a name for your rule, and leave the **Type** setting at **Regular rule**\. 

1. Change the following match settings from their defaults: 

   1. On **Statement**, for **Inspect**, open the dropdown and choose the web request component **Body**\. 

   1. For **Match type**, choose **Size greater than**\. 

   1. For **Size**, type `8192`\. 

1. For **Action**, select **Block**\.

1. Choose **Add rule**\.

1. After you add the rule, on the **Set rule priority** page, move your size constraint rule above any rules or rule groups in your web ACL that have web request body inspection\. This gives the size constraint rule a lower priority setting\. AWS WAF evaluates rules in order of priority, starting from the lowest numeric setting, so it will enforce the size constraint before inspecting the request body\. 

If you need to allow bodies that are larger than 8 KB for some requests, add a rule that explicitly allows those requests and prioritize it to run in your web ACL before your size constraint rule\. 