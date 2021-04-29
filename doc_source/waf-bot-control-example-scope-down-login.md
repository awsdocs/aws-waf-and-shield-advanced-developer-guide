# AWS WAF Bot Control example: Use Bot Control only for login page<a name="waf-bot-control-example-scope-down-login"></a>

The following example uses a scope\-down statement to use AWS WAF Bot Control only for traffic that's coming to a website's login page that's identified by the URI path `login`\. The URI path to your login page might be different from the example, depending on your application and environment\.

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
          "Name": "CategoryVerifiedSearchEngine"
        },
        {
          "Name": "CategoryVerifiedSocialMedia"
        }
      ]
    },
    "VisibilityConfig": {
      "SampledRequestsEnabled": true,
      "CloudWatchMetricsEnabled": true,
      "MetricName": "AWS-AWSBotControl-Example"
    },
    "ScopeDownStatement": {
      "ByteMatchStatement": {
        "SearchString": "login",
        "FieldToMatch": {
          "UriPath": {}
        },
        "TextTransformations": [
          {
            "Priority": 0,
            "Type": "NONE"
          }
        ],
        "PositionalConstraint": "CONTAINS"
      }
    }
  }
}
```