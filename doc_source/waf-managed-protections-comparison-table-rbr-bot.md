# Rate limiting options in rate\-based rules and targeted Bot Control rules<a name="waf-managed-protections-comparison-table-rbr-bot"></a>

The targeted level of the AWS WAF Bot Control rule group and the AWS WAF rate\-based rule statement both provide web request rate limiting\. The following table compares the two options\.


**Comparison of options for rate\-based detection and mitigation**  

|  | AWS WAF rate\-based rule | AWS WAF Bot Control targeted rules | 
| --- | --- | --- | 
| How rate limiting is applied | Blocks traffic from IP addresses that are sending requests at too high a rate\.  | Enforces human\-like access patterns and applies dynamic rate limiting, through the use of request tokens\.  | 
| Based on historical traffic baselines?  | No  | Yes  | 
| Time required to accumulate historic traffic baselines  | N/A  | Five minutes for dynamic thresholds\. N/A for token absent\. | 
| Mitigation lag  | Usually 30\-50 seconds\. Can be up to several minutes\.  | Usually less than 10 seconds\. Can be up to several minutes\.  | 
| Mitigation targets  | IP addresses  | IP addresses and client sessions  | 
| Traffic volume level required to trigger mitigations  | Medium \- can be as low as 100 requests per 5 minutes  | Low \- intended to detect client patterns such as slow scrapers  | 
| Customizable thresholds  | Yes  | No  | 
| Default mitigation action | Console default is Block\. No default setting in the API; the setting is required\. You can set this to any valid rule action except Allow\. | The rule group rule action settings are Challenge for token absent and CAPTCHA for high volume traffic from a single client session\. You can set either of these rules to any valid rule action\.  | 
| Resiliency against highly distributed attacks  | Medium \- limited to 10,000 IP addresses  | Medium \- limited to 50,000 total between IP addresses and tokens  | 
| [AWS WAF Pricing](http://aws.amazon.com/waf/pricing/) | Included in the basic fees for AWS WAF\.  | Included in the targeted level of Bot Control intelligent threat mitigation\.  | 
| For more information | [Rate\-based rule statement](waf-rule-statement-type-rate-based.md) | [AWS WAF Bot Control rule group](aws-managed-rule-groups-bot.md) | 