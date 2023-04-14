# AWS WAF Bot Control example: Allow traffic from a bot that you control<a name="waf-bot-control-example-scope-down-your-bot"></a>

You can configure some site monitoring bots and custom bots to send custom headers\. If you want to allow traffic from these types of bots, you can configure them to add a shared secret in a header\. You then can exclude messages that have the header by adding a scope\-down statement to the AWS WAF Bot Control managed rule group statement\. 

The following example rule excludes traffic with a secret header from Bot Control inspection\.

```
{
  "Name": "AWS-AWSBotControl-Example",
  "Priority": 5,
  "Statement": {
    "ManagedRuleGroupStatement": {
      "VendorName": "AWS",
      "Name": "AWSManagedRulesBotControlRuleSet",
      "RuleActionOverrides": [],
      "ExcludedRules": []
    },
    "VisibilityConfig": {
      "SampledRequestsEnabled": true,
      "CloudWatchMetricsEnabled": true,
      "MetricName": "AWS-AWSBotControl-Example"
    },
    "ScopeDownStatement": {
      "NotStatement": {
        "Statement": {
          "ByteMatchStatement": {
            "SearchString": "YSBzZWNyZXQ=",
            "FieldToMatch": {
              "SingleHeader": {
                "Name": "x-bypass-secret"
              }
            },
            "TextTransformations": [
              {
                "Priority": 0,
                "Type": "NONE"
              }
            ],
            "PositionalConstraint": "EXACTLY"
          }
        }
      }
    }
  }
}
```