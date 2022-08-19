# Inspection of the request body, headers, and cookies<a name="web-request-body-inspection"></a>

AWS WAF does not support inspecting very large contents for the body, headers, or cookies request components\. The underlying host service has count and size limits on what it forwards to AWS WAF for inspection\. For example, the host service does not send more than 200 headers to AWS WAF, so for a web request with 205 headers, AWS WAF cannot inspect the last 5 headers\. When AWS WAF allows a web request to proceed to your protected resource, the entire web request is sent, including any contents that are outside of the count and size limits that AWS WAF was able to inspect\. 

The limitations are as follows: 
+ **`Body` and `JSON Body`** – You can inspect the first 8 KB \(8,192 bytes\) of the body of a request\. 
+ **`Headers`** – You can inspect at most the first 8 KB \(8,192 bytes\) of the request headers and at most the first 200 headers\. The content is available for inspection by AWS WAF up to the first limit reached\. 
+ **`Cookies`** – You can inspect at most the first 8 KB \(8,192 bytes\) of the request cookies and at most the first 200 cookies\. The content is available for inspection by AWS WAF up to the first limit reached\. 

When you add or update a rule that inspects any of the limited request components, you specify oversize content handling in the component specification\. For information, see [Oversize handling for request components](waf-rule-statement-oversize-handling.md)\.

When you use a managed rule group or a rule group that another account has shared with you, the rule group might have a rule that inspects a limited request component but that doesn't handle oversized contents the way you need them to be handled\. For information about AWS Managed Rules, see [AWS Managed Rules rule groups list](aws-managed-rule-groups-list.md)\. For information about other rule groups, ask your rule group provider\.

The way you handle oversize components in your web ACL can depend on a number of factors such as the expected size of your request component contents, your web ACL's default request handling, and how other rules in your web ACL match and handle requests\. 

The following are general guidelines for managing oversized web request components: 
+ If you need to allow some requests with oversize component contents, if possible, add rules to explicitly allow only those requests\. Prioritize those rules so that they run before any other rules in the web ACL that inspect the same component types\. With this approach, you won't be able to use AWS WAF to inspect the entire contents of the oversize components that you allow to pass to your protected resource\.
+ For all other requests, you can prevent any additional bytes from passing through by blocking requests that go over the limit: 
  + **Your rules and rule groups** – In your rules that inspect size limited components, configure oversize handling so that you block requests that go over the limit\. For example, if your rule blocks requests with specific header contents, you can set the oversize handling to match on any request that has oversize header content\. As another example, if your web ACL blocks requests by default and your rule allows specific header contents, then you can configure your rule's oversize handling so that it doesn't match on any request that has oversize header content\. For information about the handling options, see [Oversize handling for request components](waf-rule-statement-oversize-handling.md)\. 
  + **Rule groups that you don't manage** – To prevent rule groups that you don't manage from allowing oversize request components, you can add a separate rule that inspects the request component type and blocks requests that go over the limits\. Prioritize the rule in your web ACL so that it runs before the rule groups\. For example, you can block requests with oversize body content before any of your body inspection rules run in the web ACL\. The following procedure describes how to add this type of rule\.

**To add a rule that blocks oversized contents**

1. When you create or edit your web ACL, in the rules settings, choose **Add rules**, **Add my own rules and rule groups**, **Rule builder**, then **Rule visual editor**\. For guidance creating or editing a web ACL, see [Working with web ACLs](web-acl-working-with.md)\.

1. Enter a name for your rule, and leave the **Type** setting at **Regular rule**\. 

1. Change the following match settings from their defaults: 

   1. On **Statement**, for **Inspect**, open the dropdown and choose the web request component that you need, either **Body**, **Headers**, or **Cookies**\. 

   1. For **Match type**, choose **Size greater than**\. 

   1. For **Size**, type a number that's at least `8192`\. 

   1. For **Oversize handling**, select **Match**\. 

1. For **Action**, select **Block**\.

1. Choose **Add rule**\.

1. After you add the rule, on the **Set rule priority** page, move it above any rules or rule groups in your web ACL that inspect the same component type\. This gives it a lower numeric priority setting, which causes AWS WAF to evaluate it first\. For more information, see [Processing order of rules and rule groups in a web ACL](web-acl-processing-order.md)\.