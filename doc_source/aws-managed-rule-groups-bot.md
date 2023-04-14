# AWS WAF Bot Control rule group<a name="aws-managed-rule-groups-bot"></a>

VendorName: `AWS`, Name: `AWSManagedRulesBotControlRuleSet`, WCU: 50

The Bot Control managed rule group provides rules to block and manage requests from bots\. Bots can consume excess resources, skew business metrics, cause downtime, and perform malicious activities\. 

**Protection levels**  
The Bot Control managed rule group provides two levels of protection that you can choose from: 
+ **Common** – Detects a variety of self\-identifying bots, such as web scraping frameworks, search engines, and automated browsers\. Bot Control protections at this level identify common bots using traditional bot detection techniques, such as static request data analysis\. The rules label traffic from these bots and block the ones that they cannot verify\. 
+ **Targeted** – Includes the common\-level protections and adds detection for advanced bots that do not self identify\. Targeted protections use advanced detection techniques such as browser interrogation, fingerprinting, and behavior heuristics to identify bad bot traffic\. The protections target these bots using a combination of rate limiting and CAPTCHA and background browser challenges\. The rules that provide targeted protection have names that begin with `TGT_`\.

**Note**  
You can also get rate limiting with the AWS WAF rate\-based rule statement\. For a comparison, see [Rate limiting options in rate\-based rules and targeted Bot Control rules](waf-managed-protections-comparison-table-rbr-bot.md)\. 

**Using this rule group**  
This rule group is part of the intelligent threat mitigation protections in AWS WAF\. For information, see [AWS WAF intelligent threat mitigation](waf-managed-protections.md)\.

**Note**  
You are charged additional fees when you use this managed rule group\. For more information, see [AWS WAF Pricing](http://aws.amazon.com/waf/pricing/)\.

To keep your costs down and to be sure you're managing your web traffic as you want, use this rule group in accordance with the guidance at [Best practices for intelligent threat mitigation](waf-managed-protections-best-practices.md)\.

The Bot Control rule group doesn't provide versioning or SNS update notifications\. 

**Token labels**  
This rule group uses AWS WAF token management to inspect and label web requests according to the status of their AWS WAF tokens\. AWS WAF uses tokens for client session tracking and verification\. 

AWS WAF applies one of the following labels when it inspects a web request's token and challenge timestamp\. AWS WAF doesn't add labeling about the status of the CAPTCHA timestamp\. 
+ `awswaf:managed:token:accepted` – The request token is present and has an unexpired challenge timestamp\. 
+ `awswaf:managed:token:rejected` – The request token is present but is either corrupt or has an expired challenge timestamp\.
+ `awswaf:managed:token:absent` – The request doesn't have a token\.

For more information, see [AWS WAF web request tokens](waf-tokens.md)\.

**Bot Control labels**  
The Bot Control managed rule group generates labels with the namespace prefix `awswaf:managed:aws:bot-control:` followed by the custom namespace\. The rule group might add more than one label to a request\. 

Each label reflects the Bot Control rule findings: 
+ `awswaf:managed:aws:bot-control:bot:category:<category>` – The category of bot, as defined by AWS WAF, for example, `bot:category:search_engine` and `bot:category:content_fetcher`\. 
+ `awswaf:managed:aws:bot-control:bot:name:<name>` – The bot name, if one is available, for example, the custom namespaces `bot:name:slurp`, `bot:name:googlebot`, and `bot:name:pocket_parser`\. 
+ `awswaf:managed:aws:bot-control:bot:verified` – Used to indicate a verified bot\. This is used for common desirable bots, and can be useful when combined with category labels like `bot:category:search_engine` or name labels like `bot:name:googlebot`\. 
**Note**  
Bot Control uses the IP address from the web request origin\. You can’t configure it to use the AWS WAF forwarded IP configuration, to inspect a different IP address source\. If you have verified bots that route through a proxy or load balancer, you can add a rule that runs before the Bot Control rule group to help with this\. Configure your new rule to use the forwarded IP address and explicitly allow the requests from the verified bots\. For information about using forwarded IP addresses, see [Forwarded IP address](waf-rule-statement-forwarded-ip-address.md)\.
+ `awswaf:managed:aws:bot-control:signal:<signal-details>` – Used for attributes of the request that are indicative of bots that are not more commonly used or verified\. 
+ `awswaf:managed:aws:bot-control:targeted:<additional-details>` – Used by the Bot Control targeted protections\. 

You can retrieve the labels through the API by calling `DescribeManagedRuleGroup`\. The labels are listed in the `AvailableLabels` property in the response\. 

The Bot Control managed rule group applies labels to a set of verifiable bots that are commonly allowed\. The rule group doesn't block these verified bots and doesn't apply any `signal:` labels\. If you want, you can block them, or a subset of them by writing a custom rule that uses the labels applied by the Bot Control managed rule group\. For more information about this and examples, see [AWS WAF Bot Control](waf-bot-control.md)\.

## Bot Control rules listing<a name="aws-managed-rule-groups-bot-rules"></a>

The following table lists the Bot Control rules\.


| Rule name | Description | 
| --- | --- | 
| CategoryAdvertising |  Inspects for bots that are used for advertising purposes\.  Rule action, applied only to unverified bots: Block Label: `awswaf:managed:aws:bot-control:bot:category:advertising` For verified bots, the rule group takes no action, but it adds the rule labeling plus the label `awswaf:managed:aws:bot-control:bot:verified`\.   | 
| CategoryArchiver |  Inspects for bots that are used for archiving purposes\.  Rule action, applied only to unverified bots: Block  Label: `awswaf:managed:aws:bot-control:bot:category:archiver` For verified bots, the rule group takes no action, but it adds the rule labeling plus the label `awswaf:managed:aws:bot-control:bot:verified`\.   | 
| CategoryContentFetcher |  Inspects for bots that are fetching content on behalf of a user\.  Rule action, applied only to unverified bots: Block  Label: `awswaf:managed:aws:bot-control:bot:category:content_fetcher`  For verified bots, the rule group takes no action, but it adds the rule labeling plus the label `awswaf:managed:aws:bot-control:bot:verified`\.   | 
| CategoryEmailClient |  Inspects for email clients\.  Rule action, applied only to unverified bots: Block  Label: `awswaf:managed:aws:bot-control:bot:category:email_client`  For verified bots, the rule group takes no action, but it adds the rule labeling plus the label `awswaf:managed:aws:bot-control:bot:verified`\.   | 
| CategoryHttpLibrary |  Inspects for HTTP libraries that are used by bots\.  Rule action, applied only to unverified bots: Block  Label: `awswaf:managed:aws:bot-control:bot:category:http_library`  For verified bots, the rule group takes no action, but it adds the rule labeling plus the label `awswaf:managed:aws:bot-control:bot:verified`\.   | 
| CategoryLinkChecker |  Inspects for bots that check for broken links\.  Rule action, applied only to unverified bots: Block  Label: `awswaf:managed:aws:bot-control:bot:category:link_checker`  For verified bots, the rule group takes no action, but it adds the rule labeling plus the label `awswaf:managed:aws:bot-control:bot:verified`\.   | 
| CategoryMiscellaneous |  Inspects for miscellaneous bots\.  Rule action, applied only to unverified bots: Block  Label: `awswaf:managed:aws:bot-control:bot:category:miscellaneous`  For verified bots, the rule group takes no action, but it adds the rule labeling plus the label `awswaf:managed:aws:bot-control:bot:verified`\.   | 
| CategoryMonitoring |  Inspects for bots that are used for monitoring purposes\.  Rule action, applied only to unverified bots: Block  Label: `awswaf:managed:aws:bot-control:bot:category:monitoring`  For verified bots, the rule group takes no action, but it adds the rule labeling plus the label `awswaf:managed:aws:bot-control:bot:verified`\.   | 
| CategoryScrapingFramework |  Inspects for web scraping frameworks\.  Rule action, applied only to unverified bots: Block  Label: `awswaf:managed:aws:bot-control:bot:category:scraping_framework`  For verified bots, the rule group takes no action, but it adds the rule labeling plus the label `awswaf:managed:aws:bot-control:bot:verified`\.   | 
| CategorySearchEngine |  Inspects for search engine bots\. Rule action, applied only to unverified bots: Block  Label: `awswaf:managed:aws:bot-control:bot:category:search_engine`  For verified bots, the rule group takes no action, but it adds the rule labeling plus the label `awswaf:managed:aws:bot-control:bot:verified`\.   | 
| CategorySecurity |  Inspects for security\-related bots\.  Rule action, applied only to unverified bots: Block  Label: `awswaf:managed:aws:bot-control:bot:category:security`  For verified bots, the rule group takes no action, but it adds the rule labeling plus the label `awswaf:managed:aws:bot-control:bot:verified`\.   | 
| CategorySeo |  Inspects for bots that are used for search engine optimization\.  Rule action, applied only to unverified bots: Block  Label: `awswaf:managed:aws:bot-control:bot:category:seo`  For verified bots, the rule group takes no action, but it adds the rule labeling plus the label `awswaf:managed:aws:bot-control:bot:verified`\.   | 
| CategorySocialMedia |  Inspects for bots that are used by social media platforms to provide content summaries\.  Rule action, applied only to unverified bots: Block  Label: `awswaf:managed:aws:bot-control:bot:category:social_media`  For verified bots, the rule group takes no action, but it adds the rule labeling plus the label `awswaf:managed:aws:bot-control:bot:verified`\.   | 
| SignalAutomatedBrowser |  Inspects for indications of an automated web browser\.  Rule action: Block   | 
| SignalKnownBotDataCenter |  Inspects for data centers that are typically used by bots\.  Rule action: Block   | 
| SignalNonBrowserUserAgent |  Inspects for user agent strings that don't seem to be from a web browser\. Rule action: Block   | 
| TGT\_VolumetricIpTokenAbsent |  Inspects for 5 or more requests from a client in the last 5 minutes that don't include a valid challenge token\. For information about tokens, see [AWS WAF web request tokens](waf-tokens.md)\.   The threshold that this rule applies can vary slightly due to latency\.   This rule handles missing tokens differently from the token labeling: `awswaf:managed:token:absent`\. The token labeling labels individual requests that don't have a token\. This rule maintains a count for each client session of requests that are missing their token and it matches against clients that go over the limit\. It's possible for this rule to match on a request that has a token if requests from the same client have recently been missing tokens\.  Rule action, applied only to clients that are not verified bots: Challenge  Label: `awswaf:managed:aws:bot-control:targeted:aggregate:volumetric:ip:token_absent` For verified bots, the rule group takes no action, but it adds the rule labeling plus the label `awswaf:managed:aws:bot-control:bot:verified`\.  This rule is different from the token labeling: `awswaf:managed:token:absent`, which just labels individual requests that don't have a token\. This rule maintains a count for each client session of requests that are missing their token and it takes action against unverified bots that go over the limit\.   | 
| TGT\_VolumetricSession |  Inspects for an abnormally high number of requests from a client session\. The evaluation is based on a comparison to standard volumetric baselines that AWS WAF maintains using historic traffic patterns\.  This inspection only applies when the web request has a token\. Tokens are added to requests by the application integration SDKs and by the rule actions CAPTCHA and Challenge\. For more information, see [AWS WAF web request tokens](waf-tokens.md)\. Rule action, applied only to clients that are not verified bots: CAPTCHA  Label: `awswaf:managed:aws:bot-control:targeted:aggregate:volumetric:session:high` The rule group applies the following labels to medium volume and lower volume requests that are above a minimum threshold\. For these levels, the rule takes no action, regardless of whether the client is verified: `awswaf:managed:aws:bot-control:targeted:aggregate:volumetric:session:medium` and `awswaf:managed:aws:bot-control:targeted:aggregate:volumetric:session:low`\. For verified bots, the rule group takes no action, but it adds the rule labeling plus the label `awswaf:managed:aws:bot-control:bot:verified`\.   | 
| TGT\_SignalAutomatedBrowser |  Inspects for browser automation frameworks\.  This inspection only applies when the web request has a token\. Tokens are added to requests by the application integration SDKs and by the rule actions CAPTCHA and Challenge\. For more information, see [AWS WAF web request tokens](waf-tokens.md)\. Rule action, applied only to clients that are not verified bots: CAPTCHA  Label: `awswaf:managed:aws:bot-control:targeted:signal:automated_browser` For verified bots, the rule group takes no action, but it adds the rule labeling plus the label `awswaf:managed:aws:bot-control:bot:verified`\.   | 
| TGT\_SignalBrowserInconsistency |  Inspects for inconsistent browser interrogation data\.  This inspection only applies when the web request has a token\. Tokens are added to requests by the application integration SDKs and by the rule actions CAPTCHA and Challenge\. For more information, see [AWS WAF web request tokens](waf-tokens.md)\. Rule action, applied only to clients that are not verified bots: CAPTCHA  Label: `awswaf:managed:aws:bot-control:targeted:signal:browser_inconsistency` For verified bots, the rule group takes no action, but it adds the rule labeling plus the label `awswaf:managed:aws:bot-control:bot:verified`\.   | 