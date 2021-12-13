# Customizing web requests and responses in AWS WAF<a name="waf-custom-request-response"></a>

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

**Eventual consistency**  
When you make changes to web ACLs or web ACL components, like rules and rule groups, AWS WAF propagates the changes everywhere that the web ACL and its components are stored and used\. Your changes are applied within seconds, but there might be a brief period of inconsistency when the changes have arrived in some places and not in others\. So, for example, if you change a rule action setting, the action might be the old action in one area and the new action in another area\. Or if you add an IP address to an IP set used in a blocking rule, the new address might briefly be blocked in one area while still allowed in another\. This temporary inconsistency can occur when you first associate a web ACL with an AWS resource and when you change a web ACL that is already associated with a resource\. Generally, any inconsistencies of this type last only a few seconds\.

**Maximum settings for custom request and response handling**  
For information about maximum settings for custom request and response handling, see [AWS WAF quotas](limits.md)\.

**Topics**
+ [Custom request header insertions for allow, count, and CAPTCHA actions](customizing-the-incoming-request.md)
+ [Custom responses for block actions](customizing-the-response-for-blocked-requests.md)
+ [Supported status codes for custom response](customizing-the-response-status-codes.md)