# AWS WAF client application integration<a name="waf-application-integration"></a>

AWS WAF provides application integration SDKs for you to implement in your client applications when you use an AWS Managed Rules rule group that enables advanced managed integration\. The rule groups of this kind either require an SDK integration, or provide security capabilities that are enhanced by the integration\. Currently, this functionality is available with the AWS Managed Rules rule group `AWSManagedRulesATPRuleSet`, and the integration SDKs are optional, but strongly encouraged\. For information about this rule group, see [AWS WAF Fraud Control account takeover prevention \(ATP\)](waf-atp.md) and [AWS WAF Fraud Control account takeover prevention \(ATP\) rule group](aws-managed-rule-groups-atp.md)\.

The integration SDKs manage token authorization for your client applications, and help ensure that login attempts to your protected resource are only allowed after the client has acquired a valid token\. Additionally, the SDKs gather information about the client to determine whether it's being operated by a bot or by a human being\. 

**Note**  
The ATP managed rule group currently doesn't block requests that are missing tokens\. In order to block requests that are missing tokens, after you've implemented your application integration SDK, follow the guidance at [Blocking login requests that don't have a token](waf-application-integration-block-missing-tokens.md)\. 

The JavaScript SDK is generally available, and you can use it for your browsers and other devices that execute JavaScript\. AWS WAF also offers custom SDKs for Android and iOS mobile apps\. For access to the mobile SDKs, contact sales at [Contact AWS](http://aws.amazon.com/contact-us)\.

The application integration SDKs work with web ACLs that use the rule group `AWSManagedRulesATPRuleSet`\. To add this managed rule group to your web ACL, follow the procedure at [Using the ATP managed rule group](waf-atp-rg-using.md)\.

**To access the application integration SDKs through the console**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. Choose **Application integration** in the navigation pane\. 

1. In the **Application integration SDKs** page, you can see the following: 
   + The web ACLs that are enabled for managed application integration\. Each web ACL that uses an AWS Managed Rules rule group with managed integration support is listed\. When you implement an SDK, you use the integration URL for the web ACL that you want to integrate with\.
   + The SDKs that you have access to\. The JavaScript SDK is always available\. For access to the mobile SDKs, contact sales at [Contact AWS](http://aws.amazon.com/contact-us)\.

To implement an SDK, follow the guidance for the SDK type\. After you've implemented your SDK, to block requests that are missing tokens, follow the guidance at [Blocking login requests that don't have a token](waf-application-integration-block-missing-tokens.md)\. 

**Topics**
+ [AWS WAF JavaScript SDK](waf-javascript-sdk.md)
+ [AWS WAF mobile SDK](waf-mobile-sdk.md)
+ [Blocking login requests that don't have a token](waf-application-integration-block-missing-tokens.md)