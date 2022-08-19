# AWS WAF Bot Control rule group<a name="aws-managed-rule-groups-bot"></a>

The Bot Control managed rule group available from AWS Managed Rules\.

VendorName: `AWS`, Name: `AWSManagedRulesBotControlRuleSet`, WCU: 50

The Bot Control managed rule group contains rules to block and manage requests from bots\. You are charged additional fees when you use this rule group\. For more information, see [AWS WAF Pricing](http://aws.amazon.com/waf/pricing/)\. In order to keep your costs down and to be sure you're managing your bot traffic as you want, use this rule group in accordance with the guidance at [AWS WAF Bot Control](waf-bot-control.md)\.

The Bot Control rule group doesn't provide versioning or SNS update notifications\. 

The Bot Control managed rule group generates labels with the namespace prefix `awswaf:managed:aws:bot-control:` followed by the custom namespace\. Each label reflects the Bot Control rule findings\. 
+ `awswaf:managed:aws:bot-control:bot:category:<category>` – The category of bot, as defined by AWS WAF, for example `bot:category:search_engine` and `bot:category:content_fetcher`\. 
+ `awswaf:managed:aws:bot-control:bot:name:<name>` – The bot name, if one is available, for example the custom namespaces `bot:name:slurp`, `bot:name:googlebot`, and `bot:name:pocket_parser`\. 
+ `awswaf:managed:aws:bot-control:bot:verified` – Used to indicate a verified bot\. This is used for common desirable bots, and can be useful when combined with category labels like `bot:category:search_engine` or name labels like `bot:name:googlebot`\. 

  Bot Control uses the IP addresses from AWS WAF to verify bots\. If you have verified bots that route through a proxy or load balancer, you might need to explicitly allow them\. For information, see [Forwarded IP address](waf-rule-statement-forwarded-ip-address.md)\.
+ `awswaf:managed:aws:bot-control:signal:<signal-details>` – Used for attributes of the request that are indicative of bots that are not more commonly used or verified\. 

You can retrieve the labels through the API by calling `DescribeManagedRuleGroup`\. The labels are listed in the `AvailableLabels` property in the response\. 

The Bot Control managed rule group applies labels to a set of verifiable bots that are commonly allowed\. The rule group doesn't block verified bots and doesn't apply any `signal:` labels\. If you want, you can block them, or a subset of them, by writing a custom rule that uses the labels applied by the Bot Control managed rule group\. For more information about this and examples, see [AWS WAF Bot Control](waf-bot-control.md)\.

The following table lists the Bot Control rules\.


| Rule name | Description | 
| --- | --- | 
| CategoryAdvertising |  Inspects for bots that are used for advertising purposes\.  Rule action for verified bots in this category: `Count`  Rule action for unverified bots in this category: `Block`   | 
| CategoryArchiver |  Inspects for bots that are used for archiving purposes\.  Rule action for verified bots in this category: `Count`  Rule action for unverified bots in this category: `Block`   | 
| CategoryContentFetcher |  Inspects for bots that are fetching content on behalf of a user\.  Rule action for verified bots in this category: `Count`  Rule action for unverified bots in this category: `Block`   | 
| CategoryEmailClient |  Inspects for email clients\.  Rule action for verified bots in this category: `Count`  Rule action for unverified bots in this category: `Block`   | 
| CategoryHttpLibrary |  Inspects for HTTP libraries that are often used by bots\.  Rule action for verified bots in this category: `Count`  Rule action for unverified bots in this category: `Block`   | 
| CategoryLinkChecker |  Inspects for bots that check for broken links\.  Rule action for verified bots in this category: `Count`  Rule action for unverified bots in this category: `Block`   | 
| CategoryMiscellaneous |  Inspects for miscellaneous bots\.  Rule action for verified bots in this category: `Count`  Rule action for unverified bots in this category: `Block`   | 
| CategoryMonitoring |  Inspects for bots that are used for monitoring purposes\.  Rule action for verified bots in this category: `Count`  Rule action for unverified bots in this category: `Block`   | 
| CategoryScrapingFramework |  Inspects for web scraping frameworks\.  Rule action for verified bots in this category: `Count`  Rule action for unverified bots in this category: `Block`   | 
| CategorySearchEngine |  Inspects for search engine bots\.  Rule action for verified bots in this category: `Count`  Rule action for unverified bots in this category: `Block`   | 
| CategorySecurity |  Inspects for security\-related bots\.  Rule action for verified bots in this category: `Count`  Rule action for unverified bots in this category: `Block`   | 
| CategorySeo |  Inspects for bots that are used for search engine optimization\.  Rule action for verified bots in this category: `Count`  Rule action for unverified bots in this category: `Block`   | 
| CategorySocialMedia |  Inspects for bots that are used by social media platforms to provide content summaries\. Rule action for verified bots in this category: `Count`  Rule action for unverified bots in this category: `Block`   | 
| SignalAutomatedBrowser |  Inspects for indications of an automated web browser\.  Rule action: `Block`   | 
| SignalKnownBotDataCenter |  Inspects for data centers that are typically used by bots\.  Rule action: `Block`   | 
| SignalNonBrowserUserAgent |  Inspects for user agent strings that don't seem to be from a web browser\. Rule action: `Block`   | 