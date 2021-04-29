# AWS WAF Bot Control example: Block verified bots<a name="waf-bot-control-example-block-verified-bots"></a>

In order to block verified bots, you must add a rule to block them that runs after the AWS WAF Bot Control managed rule group\. To do this, identify the bot names that you want to block and use a label match statement to identify and block them\. If you want to just block all verified bots, you can omit the match against the `bot:name:` label\. 

The following rule blocks only the `bingbot` verified bot\. This rule must run after the Bot Control managed rule group\.

```
{
  "Rule": {
    "Name": "match_rule",
    "Statement": {
      "AndStatement": {
        "Statements": [
          {
            "LabelMatchStatement": {
              "Scope": "LABEL",
              "Key": "awswaf:managed:aws:bot-control:bot:name:bingbot"
            }
          },
          {
            "LabelMatchStatement": {
              "Scope": "LABEL",
              "Key": "awswaf:managed:aws:bot-control:bot:verified"
            }
          }
        ]
      }
    },
    "RuleLabels": [],
    "Action": {
      "Block": {}
    }
  }
}
```

The following rule blocks all verified bots\.

```
{
  "Rule": {
    "Name": "match_rule",
    "Statement": {
      "LabelMatchStatement": {
        "Scope": "LABEL",
        "Key": "awswaf:managed:aws:bot-control:bot:verified"
      }
    },
    "RuleLabels": [],
    "Action": {
      "Block": {}
    }
  }
}
```