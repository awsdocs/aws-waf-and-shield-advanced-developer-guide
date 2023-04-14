# Options for intelligent threat mitigation<a name="waf-managed-protections-comparison-table"></a>

This section provides a detailed comparison of the options for implementing intelligent threat mitigation\. 

AWS WAF offers the following types of protections for intelligent threat mitigation\.
+ **AWS WAF Fraud Control account takeover prevention \(ATP\)** – Detects and manages malicious takeover attempts on your application's login page\. The core functionality is provided by the ATP managed rule group\. For more information, see [AWS WAF Fraud Control account takeover prevention \(ATP\)](waf-atp.md) and [AWS WAF Fraud Control account takeover prevention \(ATP\) rule group](aws-managed-rule-groups-atp.md)\.
+ **AWS WAF Bot Control** – Identifies, labels, and manages both friendly and malicious bots\. This feature provides management for common bots with signatures that are unique across applications, and also for targeted bots that have signatures specific to an application\. The core functionality is provided by the Bot Control managed rule group\. For more information, see [AWS WAF Bot Control](waf-bot-control.md) and [AWS WAF Bot Control rule group](aws-managed-rule-groups-bot.md)\.
+ **Client application integration SDKs** – Validate client sessions and acquire AWS WAF tokens for clients to use in their web requests\. If you use ATP or Bot Control, implement the application integration SDKs in your client application if you can, to take full advantage of all of the rule group features\. We only recommend using these rule groups without an SDK integration as a temporary measure, when a critical resource needs to be quickly secured and there isn’t enough time for the SDK integration\. For information about implementing the SDKs, see [AWS WAF client application integration](waf-application-integration.md)\. 
+ **Challenge and CAPTCHA rule actions** – Validate client sessions and end users and acquire AWS WAF tokens for clients to use in their web requests\. You can implement these anywhere that you specify a rule action, in your rules and as overrides in rule groups that you use\. These actions use AWS WAF JavaScript interstitials to interrogate the client or end user, and they require client applications that support JavaScript\. For more information, see [CAPTCHA and Challenge actions in AWS WAF](waf-captcha-and-challenge.md)\.

The ATP and Bot Control managed rule groups use tokens for advanced detection\. For information about the features that tokens enable in the rule groups, see [Why you should use the application integration SDKs with ATP](waf-atp-with-tokens.md) and [Why you should use the application integration SDKs with Bot Control](waf-bot-with-tokens.md)\. 

Your options for implementing intelligent threat mitigation run from the basic use of rule actions to run challenges and enforce token acquisition, to the advanced features offered by the Bot Control and ATP AWS Managed Rules rule groups\.

The following tables provide detailed comparisons of the options for the basic and advanced features\. 

**Topics**
+ [Challenges and token acquisition](waf-managed-protections-comparison-table-token.md)
+ [Bot Control and ATP managed rule groups](waf-managed-protections-comparison-table-rg.md)
+ [Rate limiting options in rate\-based rules and targeted Bot Control rules](waf-managed-protections-comparison-table-rbr-bot.md)