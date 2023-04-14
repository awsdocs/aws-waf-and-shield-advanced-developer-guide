# Adding the AWS WAF Bot Control managed rule group to your web ACL<a name="waf-bot-control-rg-using"></a>

The Bot Control managed rule group `AWSManagedRulesBotControlRuleSet` requires additional configuration to identify the protection level that you want to implement\. 

For the rule group description and rules listing, see [AWS WAF Fraud Control account takeover prevention \(ATP\) rule group](aws-managed-rule-groups-atp.md)\.

This guidance is intended for users who know generally how to create and manage AWS WAF web ACLs, rules, and rule groups\. Those topics are covered in prior sections of this guide\. 

**Follow best practices**  
Use the Bot Control rule group in accordance with the best practices at [Best practices for intelligent threat mitigation](waf-managed-protections-best-practices.md)\. 

**To use the `AWSManagedRulesBotControlRuleSet` rule group in your web ACL**

1. Add the AWS managed rule group, `AWSManagedRulesBotControlRuleSet` to your web ACL\. For the full rule group description, see [AWS WAF Bot Control rule group](aws-managed-rule-groups-bot.md)\. 
**Note**  
You are charged additional fees when you use this managed rule group\. For more information, see [AWS WAF Pricing](http://aws.amazon.com/waf/pricing/)\.

   When you add the rule group, edit it to open the configuration page for the rule group\. 

1. On the rule group's configuration page, in the **Inspection level** pane, select the inspection level that you want to use\. 
   + **Common** – Detects a variety of self\-identifying bots, such as web scraping frameworks, search engines, and automated browsers\. Bot Control protections at this level identify common bots using traditional bot detection techniques, such as static request data analysis\. The rules label traffic from these bots and block the ones that they cannot verify\. 
   + **Targeted** – Includes the common\-level protections and adds detection for advanced bots that do not self identify\. Targeted protections use advanced detection techniques such as browser interrogation, fingerprinting, and behavior heuristics to identify bad bot traffic\. The protections target these bots using a combination of rate limiting and CAPTCHA and background browser challenges\. The rules that provide targeted protection have names that begin with `TGT_`\.

   For more information about this choice, see [AWS WAF Bot Control rule group](aws-managed-rule-groups-bot.md)\.

1. Add a scope\-down statement for the rule group, to contain the costs of using it\. A scope\-down statement narrows the set of requests that the rule group inspects\. For example use cases, start with [AWS WAF Bot Control example: Use Bot Control only for the login page](waf-bot-control-example-scope-down-login.md) and [AWS WAF Bot Control example: Use Bot Control only for dynamic content](waf-bot-control-example-scope-down-dynamic-content.md)\. 

1. Provide any additional configuration that you need for the rule group\. 

1. Save your changes to the web ACL\. 

Before you deploy your Bot Control implementation for production traffic, test and tune it in a staging or testing environment until you are comfortable with the potential impact to your traffic\. Then test and tune the rules in count mode with your production traffic before enabling them\. See the sections that follow for guidance\. 