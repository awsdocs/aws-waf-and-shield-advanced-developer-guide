# Custom request header insertions for allow, count, and CAPTCHA actions<a name="customizing-the-incoming-request"></a>

You can instruct AWS WAF to insert custom headers into the original HTTP request when it permits the request to go through\. You can only add to the request\. You can't modify or replace any part of the original request\. 

This option applies to rule actions that are set to allow, count, or CAPTCHA and to web ACL default actions that are set to allow\. For more information about rule actions, see [AWS WAF rule action](waf-rule-action.md)\. For more information about default web ACL actions, see [Deciding on the default action for a web ACL](web-acl-default-action.md)\.

Use cases for custom header insertion include signaling a downstream application to process the request differently based on the inserted headers, and flagging the request for analysis\.

**Custom request header names**  
AWS WAF prefixes all request headers that it inserts with `x-amzn-waf-`, to avoid confusion with the headers that are already in the request\. For example, if you specify the header name `sample`, AWS WAF inserts the header `x-amzn-waf-sample`\. 

**Headers with the same name**  
If the request already has a header with the same name that AWS WAF is inserting, AWS WAF overwrites the header\. So, if you define headers in multiple rules with identical names, the last rule to inspect the request and find a match would have its header added, and any previous rules would not\. 

**Custom headers with the count or CAPTCHA action**  
The count and CAPTCHA rule actions don't stop AWS WAF from processing the web request\. If you insert custom headers with a rule that uses these actions, subsequent rules might also insert custom headers\. For information about rule action behavior, see [AWS WAF rule action](waf-rule-action.md)\.

For example, suppose you have the following rules, prioritized in the order shown: 

1. RuleA with a count action and a customized header named `RuleAHeader`\.

1. RuleB with an allow action and a customized header named `RuleBHeader`\.

If a request matches both RuleA and RuleB, AWS WAF inserts the headers `x-amzn-waf-RuleAHeader` and `x-amzn-waf-RuleBHeader`, and then forwards the request to the protected resource\. 

AWS WAF inserts custom headers into a web request when it finishes inspecting the request\. So if you use custom request handling with a rule that has the action set to count, the custom headers that you add are not inspected by subsequent rules\. 

**Example custom request handling**  
You define custom request handling for a rule's action or for a web ACL's default action\. The following listing shows the JSON for custom handling added to the default action for a web ACL\. 

```
{
 "Name": "SampleWebACL",
 "Scope": "REGIONAL",
 "DefaultAction": {
  "Allow": {
   "CustomRequestHandling": {
    "InsertHeaders": [
     {
      "Name": "fruit",
      "Value": "watermelon"
     },
     {
      "Name": "pie",
      "Value": "apple"
     }
    ]
   }
  }
 },
 "Description": "Sample web ACL with custom request handling configured for default action.",
 "Rules": [],
 "VisibilityConfig": {
  "SampledRequestsEnabled": true,
  "CloudWatchMetricsEnabled": true,
  "MetricName": "SampleWebACL"
 }
}
```