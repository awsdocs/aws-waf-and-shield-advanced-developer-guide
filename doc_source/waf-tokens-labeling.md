# Token labeling by the Bot Control and ATP managed rule groups<a name="waf-tokens-labeling"></a>

When you use the ATP and Bot Control AWS Managed Rules rule groups, the rule groups use AWS WAF token management to inspect web request tokens and apply token labeling to the requests\. 

**Note**  
AWS WAF token management only applies token labels when you use the Bot Control or ATP managed rule group\.

AWS WAF applies one of the following labels when it inspects a web request's token and challenge timestamp\. AWS WAF doesn't add labeling about the status of the CAPTCHA timestamp\. 
+ `awswaf:managed:token:accepted` – The request token is present and has an unexpired challenge timestamp\. 
+ `awswaf:managed:token:rejected` – The request token is present but is either corrupt or has an expired challenge timestamp\.
+ `awswaf:managed:token:absent` – The request doesn't have a token\.

You can add your own rules after either of these managed rule groups in your web ACL, to match against the token labels\. For information about label matching in your rules, see [Matching against a label](waf-rule-label-match.md)\. 

For information about the managed rule groups and the labels that their rules add to web requests, see [AWS WAF Bot Control rule group](aws-managed-rule-groups-bot.md) and [AWS WAF Fraud Control account takeover prevention \(ATP\) rule group](aws-managed-rule-groups-atp.md)\.