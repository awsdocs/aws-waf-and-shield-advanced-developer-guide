# AWS WAF Bot Control example: Allow a specific blocked bot<a name="waf-bot-control-example-allow-blocked-bot"></a>

If AWS WAF Bot Control is blocking a bot that you do not want to block, do the following:

1. Identify the Bot Control rule that's blocking the bot by checking the logs\. For information about the web ACL logs, see [Logging web ACL traffic information](logging.md)\. Note any identifying features like labels and user agent\. 

1. In your web ACL, exclude the rule that's blocking the bot from the rule group\. To do this in the console, you edit the rule group inside the web ACL and set the blocking rule to count\. This ensures that the bot is not blocked, while still allowing the rule to apply its label to matching requests\. 

   At this point, you've configured the web ACL to stop blocking all bots that are normally blocked by the Bot Control rule\. 

1. Add a custom label matching rule to your web ACL, after the Bot Control managed rule group\. Configure the rule to match against the Bot Control rule label and to block all matching requests except for the bot that you don't want to block\. 

   Your web ACL is now configured so that the bot you wanted to allow is no longer blocked by the Bot Control managed rule group\.

For example, suppose you want to block all monitoring bots except for `pingdom`\. In this case, you exclude the `CategoryMonitoring` rule and then write a rule to block all monitoring bots except for those with the bot name label `pingdom`\. 

The following rule uses the Bot Control managed rule group but changes the rule action for `CategoryMonitoring` to count, by excluding it from normal rule group processing\. The category monitoring rule applies its labels as usual to matching requests, but only counts them instead of performing its usual action of block\. 

```
{
  "Name": "AWS-AWSBotControl-Example",
  "Priority": 5,
  "Statement": {
    "ManagedRuleGroupStatement": {
      "VendorName": "AWS",
      "Name": "AWSManagedRulesBotControlRuleSet",
      "ExcludedRules": [
        {
          "Name": "CategoryMonitoring"
        }
      ]
    }
  },
  "VisibilityConfig": {
    "SampledRequestsEnabled": true,
    "CloudWatchMetricsEnabled": true,
    "MetricName": "AWS-AWSBotControl-Example"
  }
}
```

The following rule matches against the category monitoring label that the preceding `CategoryMonitoring` rule adds to matching web requests\. Among the category monitoring requests, this rule blocks all but those that have a label for the bot name `pingdom`\. 

The following rule must run after the preceding Bot Control managed rule group in the web ACL processing order\. 

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
              "Key": "awswaf:managed:aws:bot-control:bot:category:monitoring"
            }
          },
          {
            "NotStatement": {
              "Statement": {
                "LabelMatchStatement": {
                  "Scope": "LABEL",
                  "Key": "awswaf:managed:aws:bot-control:bot:name:pingdom"
                }
              }
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