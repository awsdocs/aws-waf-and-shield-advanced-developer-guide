# AWS WAF Bot Control example: Allow a specific blocked bot<a name="waf-bot-control-example-allow-blocked-bot"></a>

It's possible for a bot to be blocked by more than one of the Bot Control rules\. Run through the following procedure for each blocking rule\. 

If a AWS WAF Bot Control rule is blocking a bot that you do not want to block, do the following:

1. Identify the Bot Control rule that's blocking the bot by checking the logs\. The blocking rule will be specified in the logs in the fields whose names start with `terminatingRule`\. For information about the web ACL logs, see [Logging web ACL traffic](logging.md)\. Note the label that the rule is adds to the requests\. 

1. In your web ACL, override the action of the blocking rule to count\. To do this in the console, edit the rule group rule in the web ACL and choose a rule action override of Count for the rule\. This ensures that the bot is not blocked by the rule, but the rule will still apply its label to matching requests\. 

1. Add a label matching rule to your web ACL, after the Bot Control managed rule group\. Configure the rule to match against the overridden rule's label and to block all matching requests except for the bot that you don't want to block\. 

   Your web ACL is now configured so that the bot you want to allow is no longer blocked by the blocking rule that you identified through the logs\. 

Check traffic and your logs again, to be sure that the bot is being allowed through\. If not, run through the above procedure again\.

For example, suppose you want to block all monitoring bots except for `pingdom`\. In this case, you override the `CategoryMonitoring` rule to count and then write a rule to block all monitoring bots except for those with the bot name label `pingdom`\. 

The following rule uses the Bot Control managed rule group but overrides the rule action for `CategoryMonitoring` to count\. The category monitoring rule applies its labels as usual to matching requests, but only counts them instead of performing its usual action of block\. 

```
{
  "Name": "AWS-AWSBotControl-Example",
  "Priority": 5,
  "Statement": {
    "ManagedRuleGroupStatement": {
      "VendorName": "AWS",
      "Name": "AWSManagedRulesBotControlRuleSet",
      "RuleActionOverrides": [
        {
          "ActionToUse": {
            "Count": {}
          },
          "Name": "CategoryMonitoring"
        }
      ],
      "ExcludedRules": []
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
      "Name": "match_rule",
      "Priority": 10,
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
      "Action": {
        "Block": {}
      },
      "VisibilityConfig": {
        "SampledRequestsEnabled": true,
        "CloudWatchMetricsEnabled": true,
        "MetricName": "match_rule"
      }
}
```