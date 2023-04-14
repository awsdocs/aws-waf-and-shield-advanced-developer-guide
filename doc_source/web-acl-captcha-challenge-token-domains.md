# CAPTCHA, challenge, and token domain configuration for a web ACL<a name="web-acl-captcha-challenge-token-domains"></a>

You can configure options in your web ACL for the rules that use the CAPTCHA or Challenge rule actions and for the application integration SDKs that manage silent client challenges for AWS WAF managed protections\. 

These features mitigate bot activity by challenging end users with CAPTCHA puzzles and by presenting client sessions with silent challenges\. When the client responds successfully, AWS WAF provides a token for them to use in their web request, timestamped with the last successful puzzle and challenge responses\. For more information, see [AWS WAF intelligent threat mitigation](waf-managed-protections.md)\.

In your web ACL configuration, you can configure how AWS WAF manages these tokens: 
+ **CAPTCHA and challenge immunity times** – These specify how long a CAPTCHA or challenge timestamp remains valid\. The web ACL settings are inherited by all rules that don't have their own immunity time settings configured and also by the application integration SDKs\. For more information, see [Timestamp expiration: token immunity times](waf-tokens-immunity-times.md)\.
+ **Token domains** – By default, AWS WAF accepts tokens only for the domain of the resource that the web ACL is associated with\. If you configure a token domain list, AWS WAF accepts tokens for all domains in the list and for the domain of the associated resource\. For more information, see [Configuring the web ACL token domain list](waf-tokens-domains.md#waf-tokens-domain-lists)\.