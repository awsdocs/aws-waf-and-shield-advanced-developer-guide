# Bot Control and ATP managed rule groups<a name="waf-managed-protections-comparison-table-rg"></a>

The AWS Managed Rules rule groups that provide intelligent threat mitigation include management of basic bots, detection and mitigation of advanced, malicious bots, and detection and mitigation of account takeover attempts\. These rule groups, combined with the application integration SDKS described in the prior section, provide the most advanced protections and secure coupling with your client applications\. 


**Comparison of the managed rules group options**  

|  | Bot Control common level | Bot Control targeted level | ATP  | 
| --- | --- | --- | --- | 
| What it is | Manages common bots that self\-identify, with signatures that are unique across applications\.See [AWS WAF Bot Control rule group](aws-managed-rule-groups-bot.md)\. | Manages targeted bots that don't self\-identify, with signatures that are specific to an application\.See [AWS WAF Bot Control rule group](aws-managed-rule-groups-bot.md)\. | Manages requests that might be part of malicious takeover attempts on an application's login page\.Does not manage bots\. See [AWS WAF Fraud Control account takeover prevention \(ATP\) rule group](aws-managed-rule-groups-atp.md)\. | 
| Good choice for\.\.\. | Basic bot protection and labeling of common, automated bot traffic\. | Targeted protection against advanced bots, including rate limiting at the client session level and detection and mitigation of browser automation tools such as Selenium and Puppeteer\. | Inspection of login traffic for account takeover attacks such login attempts with password traversal and many login attempts from the same IP address\. When used with tokens, also provides aggregate protections such as rate limiting for high volume traffic at the IP and client session levels\. | 
| Adds labels that indicate evaluation results | Yes | Yes | Yes | 
| Adds token labels | Yes | Yes | Yes | 
| Blocking for requests that don't have a valid token | Not included\. See [Blocking requests that don't have a valid token](waf-tokens-block-missing-tokens.md)\. | Blocks client sessions that send 5 requests without a token\. | Not included\. See [Blocking requests that don't have a valid token](waf-tokens-block-missing-tokens.md)\. | 
| Requires the AWS WAF token aws\-waf\-token | No | Yes | Required for many rules\.See [Why you should use the application integration SDKs with ATP](waf-atp-with-tokens.md)\. | 
| Acquires the AWS WAF token aws\-waf\-token | No | Some rules use Challenge or CAPTCHA rule actions, which acquire tokens\. | No | 

For details about costs associated with these options, see the intelligent threat mitigation information at [AWS WAF Pricing](http://aws.amazon.com/waf/pricing/)\.