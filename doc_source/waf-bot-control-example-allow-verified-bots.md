# AWS WAF Bot Control example: Explicitly allow verified bots<a name="waf-bot-control-example-allow-verified-bots"></a>

AWS WAF Bot Control doesn't block bots that are known by AWS to be common and verifiable bots\. When Bot Control identifies a web request as coming from a verified bot, it adds a label that names the bot and a label that indicates that it's a verified bot\. Bot Control doesn't add any other labels, such as signals labels, in order to prevent known good bots from being blocked\.

You might have other AWS WAF rules that block verified bots\. If you want to ensure that verified bots are allowed, add a custom rule to allow them based on the Bot Control labels\. Your new rule must run after the Bot Control managed rule group, so that the labels are available to match against\. 

The following rule explicitly allows verified bots\.

```
{
    "Name": "match_rule",
    "Statement": {
      "LabelMatchStatement": {
        "Scope": "LABEL",
        "Key": "awswaf:managed:aws:bot-control:bot:verified"
      }
    },
    "RuleLabels": [],
    "Action": {
      "Allow": {}
    }
}
```