# AWS WAF web request tokens<a name="waf-tokens"></a>

AWS WAF tokens are an integral part of the enhanced protections offered by AWS WAF intelligent threat mitigation\. A token, sometimes called a fingerprint, is a collection of information about a single client session that the client stores and provides with every web request\. AWS WAF uses tokens to identify and separate malicious client sessions from legitimate sessions, even when both originate from a single IP address\. Token use imposes costs that are negligible for legitimate users, but expensive at scale for botnets\. 

AWS WAF uses tokens to support its browser and end user challenge functionality, which is provided by the application integration SDKs and by the rule actions Challenge and CAPTCHA\. Additionally, tokens enable features of the AWS WAF Bot Control and account takeover prevention managed rule groups\.

AWS WAF creates, updates, and encrypts tokens for clients that successfully respond to silent challenges and CAPTCHA puzzles\. When a client with a token sends a web request, it includes the encrypted token, and AWS WAF decrypts the token and verifies its contents\. 

**Topics**
+ [How tokens are used](waf-tokens-usage.md)
+ [Token characteristics](waf-tokens-details.md)
+ [Timestamp expiration: token immunity times](waf-tokens-immunity-times.md)
+ [Token domains and domain lists](waf-tokens-domains.md)
+ [Token labeling by the Bot Control and ATP managed rule groups](waf-tokens-labeling.md)
+ [Blocking requests that don't have a valid token](waf-tokens-block-missing-tokens.md)
+ [Configuration required for Application Load Balancers that are CloudFront origins](waf-tokens-with-alb-and-cf.md)