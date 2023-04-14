# AWS WAF client application integration<a name="waf-application-integration"></a>

Use the AWS WAF application integration SDKs to couple client\-side protections with your AWS server\-side web ACL protections, adding verifications that the client applications that send web requests to your protected resource are the intended ones\. The application SDKs verify the client application with silent challenges and provide AWS token acquisition and management, similar to the functionality provided by the AWS WAF Challenge rule action\. 

The integration SDKs manage token authorization for your client application sessions and help ensure that login attempts to your protected resource are only allowed after the client has acquired a valid token\. Additionally, the SDKs gather information about the client to help determine whether it's being operated by a bot or by a human being\. 

The application integration SDKs work with web ACLs that use the rule group `AWSManagedRulesATPRuleSet` or the targeted protection level of the rule group `AWSManagedRulesBotControlRuleSet`\. The SDKs enable the full functionality of these advanced managed rule groups\. 
+ AWS WAF Fraud Control account takeover prevention \(ATP\) managed rule group `AWSManagedRulesATPRuleSet`\. 

  Account takeover is an online illegal activity in which an attacker gains unauthorized access to a person's account\. The ATP managed rule group provides rules to block, label, and manage requests that might be part of malicious account takeover attempts\. 

  The SDKs enable fine\-tuned client verification and behavior aggregation that the ATP rules use to separate valid client traffic from malicious traffic\.

  For more information, see [AWS WAF Fraud Control account takeover prevention \(ATP\) rule group](aws-managed-rule-groups-atp.md) and [AWS WAF Fraud Control account takeover prevention \(ATP\)](waf-atp.md)\.
+ AWS WAF Bot Control managed rule group `AWSManagedRulesBotControlRuleSet`\. 

  Bots run from self\-identifying and useful ones, such as most search engines and crawlers, to malicious bots that operate against your website and don't self\-identify\. The Bot Control managed rule group provides rules to monitor, label, and manage the bot activity in your web traffic\. 

  When you use the targeted protection level of this rule group, the targeted rules use the client session information that the SDKs provide to better detect malicious bots\. 

  For more information, see [AWS WAF Bot Control rule group](aws-managed-rule-groups-bot.md) and [AWS WAF Bot Control](waf-bot-control.md)\.

To add one of these managed rule groups to your web ACL, see the procedures [Adding the AWS WAF Bot Control managed rule group to your web ACL](waf-bot-control-rg-using.md) and [Adding the ATP managed rule group to your web ACL](waf-atp-rg-using.md)\.

**Note**  
The managed rule groups currently don't block requests that are missing tokens\. In order to block requests that are missing tokens, after you implement your application integration SDK, follow the guidance at [Blocking requests that don't have a valid token](waf-tokens-block-missing-tokens.md)\. 

The JavaScript SDK is generally available, and you can use it for your browsers and other devices that execute JavaScript\. For Android and iOS mobile apps, AWS WAF also offers custom SDKs for Android versions 23 and later and iOS versions 13 and later\. 

For access to the mobile SDKs, contact sales at [Contact AWS](http://aws.amazon.com/contact-us)\.

**To access the application integration SDKs through the console**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. Choose **Application integration** in the navigation pane\. 

1. In the **Application integration SDKs** page, you can see the following: 
   + The web ACLs that are enabled for managed application integration\. Each web ACL that uses the rule group `AWSManagedRulesATPRuleSet` or the targeted protection level of the rule group `AWSManagedRulesBotControlRuleSet` is listed\. When you implement an SDK, you use the integration URL for the web ACL that you want to integrate with\.
   + The SDKs that you have access to\. The JavaScript SDK is always available\. For access to the mobile SDKs, contact sales at [Contact AWS](http://aws.amazon.com/contact-us)\.

To implement an SDK, follow the guidance for the SDK type\. After you've implemented your SDK, to block requests that are missing tokens, follow the guidance at [Blocking requests that don't have a valid token](waf-tokens-block-missing-tokens.md)\. 

**Topics**
+ [AWS WAF JavaScript SDK](waf-javascript-sdk.md)
+ [AWS WAF mobile SDK](waf-mobile-sdk.md)