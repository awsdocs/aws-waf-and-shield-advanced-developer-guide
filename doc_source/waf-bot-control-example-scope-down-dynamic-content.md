# AWS WAF Bot Control example: Use Bot Control only for dynamic content<a name="waf-bot-control-example-scope-down-dynamic-content"></a>

This example uses a scope\-down statement to apply AWS WAF Bot Control only to dynamic content\. 

The scope\-down statement excludes static content by negating the match results for a regex pattern set: 
+ The regex pattern set is configured to match extensions of *static content*\. For example, the regex pattern set specification might be `(?i)\.(jpe?g|gif|png|svg|ico|css|js|woff2?)$`\. For information about regex pattern sets and statements, see [Regex pattern set match rule statement](waf-rule-statement-type-regex-pattern-set-match.md)\. 
+ In the scope\-down statement, we exclude the matching static content by nesting the regex pattern set statement inside a `NOT` statement\. For information about the `NOT` statement, see [`NOT` rule statement](waf-rule-statement-type-not.md)\.

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
      "NotStatement": {
        "Statement": {
          "RegexPatternSetReferenceStatement": {
            "ARN": "arn:aws:wafv2:us-east-1:123456789:regional/regexpatternset/excludeset/00000000-0000-0000-0000-000000000000",
            "FieldToMatch": {
              "UriPath": {}
            },
            "TextTransformations": [
              {
                "Priority": 0,
                "Type": "NONE"
              }
            ]
          }
        }
      }
    }
  }
}
```