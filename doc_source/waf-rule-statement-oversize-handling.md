# Oversize handling for request components<a name="waf-rule-statement-oversize-handling"></a>

AWS WAF does not support inspecting very large contents for the body, headers, or cookies request components\. The underlying host service has count and size limits on what it forwards to AWS WAF for inspection\. For example, the host service does not send more than 200 headers to AWS WAF, so for a web request with 205 headers, AWS WAF cannot inspect the last 5 headers\. When AWS WAF allows a web request to proceed to your protected resource, the entire web request is sent, including any contents that are outside of the count and size limits that AWS WAF was able to inspect\. 

The limitations are as follows: 
+ **`Body` and `JSON Body`** – You can inspect the first 8 KB \(8,192 bytes\) of the body of a request\. 
+ **`Headers`** – You can inspect at most the first 8 KB \(8,192 bytes\) of the request headers and at most the first 200 headers\. The content is available for inspection by AWS WAF up to the first limit reached\. 
+ **`Cookies`** – You can inspect at most the first 8 KB \(8,192 bytes\) of the request cookies and at most the first 200 cookies\. The content is available for inspection by AWS WAF up to the first limit reached\. 

For these components, you provide oversize handling instructions when you define your rule statement\. Oversize handling tells AWS WAF what to do with a web request when the request component that the rule inspects is over the limits\. 

The options for oversize handling are the following: 
+ **`Continue`** – Inspect the request component normally according to the rule inspection criteria\. AWS WAF will inspect the request component contents that are within the size limitations\. 
+ **`Match`** – Treat the web request as matching the rule statement\. AWS WAF applies the rule action to the request without evaluating it against the rule's inspection criteria\. For a rule with `Block` action, this blocks the request with the oversize component\.
+ **`No match`** – Treat the web request as not matching the rule statement, without evaluating it against the rule's inspection criteria\. AWS WAF continues its inspection of the web request using the rest of the rules in the web ACL, like it would do for any non\-matching rule\. 

Of these three options, the `Match` option used in a rule that has a rule action of `Block` will block a request with oversize contents from proceeding to your protected resource\. With the other options, the final disposition of the request can depend on various factors, such as the configuration of the other rules in your web ACL and the web ACL's default action setting\. 

The size and count limitations apply to all rules that you use\. This includes any rules that you use but don't manage, in managed rule groups and in rule groups that are shared with you by another account\. For information about managing oversize components in those cases, see [Inspection of the request body, headers, and cookies](web-request-body-inspection.md)\.