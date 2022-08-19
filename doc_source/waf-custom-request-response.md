# Customized web requests and responses in AWS WAF<a name="waf-custom-request-response"></a>

You can add custom web request and response handling behavior to your AWS WAF rule actions and default web ACL actions\. Your custom settings apply whenever the action they're attached to applies\. 

You can customize web requests and responses in the following ways: 
+ With allow, count, and CAPTCHA actions, you can insert custom headers into the web request\. When AWS WAF forwards the web request to the protected resource, the request contains the entire original request plus the custom headers that you've inserted\. For the CAPTCHA action, AWS WAF only applies the customization if the request passes the CAPTCHA inspection\.
+ With block actions, you can define a complete custom response, with response code, headers, and body\. The protected resource responds to the request using the custom response provided by AWS WAF\. Your custom response replaces the default block action response of `403 (Forbidden)`\.

**Action settings that you can customize**  
You can specify a custom request or response when you define the following action settings: 
+ Rule action\. For information, see [AWS WAF rule action](waf-rule-action.md)\.
+ Default action for a web ACL\. For information, see [Deciding on the default action for a web ACL](web-acl-default-action.md)\.

**Action settings that you cannot customize**  
You *cannot* specify custom request handling in the override action for a rule group that you use in a web ACL\. See [Web ACL rule and rule group evaluation](web-acl-processing.md)\. Also see [Managed rule group statement](waf-rule-statement-type-managed-rule-group.md) and [Rule group statement](waf-rule-statement-type-rule-group.md)\.

**Temporary inconsistencies during updates**  
When you create or change a web ACL or other AWS WAF resources, the changes take a small amount of time to propagate to all areas where the resources are stored\. The propagation time can be from a few seconds to a number of minutes\. 

The following are examples of the temporary inconsistencies that you might notice during change propagation: 
+ After you create a web ACL, if you try to associate it with a resource, you might get an exception indicating that the web ACL is unavailable\. 
+ After you add a rule group to a web ACL, the new rule group rules might be in effect in one area where the web ACL is used and not in another\.
+ After you change a rule action setting, you might see the old action in some places and the new action in others\. 
+ After you add an IP address to an IP set that is in use in a blocking rule, the new address might be blocked in one area while still allowed in another\.

**Limits on your use of custom requests and responses**  
AWS WAF defines maximum settings for your use of custom requests and responses\. For example, a maximum number of request headers per web ACL or rule group, and a maximum number of custom headers for a single custom response definition\. For information, see [AWS WAF quotas](limits.md)\.

**Topics**
+ [Custom request header insertions for allow, count, and CAPTCHA actions](customizing-the-incoming-request.md)
+ [Custom responses for block actions](customizing-the-response-for-blocked-requests.md)
+ [Supported status codes for custom response](customizing-the-response-status-codes.md)