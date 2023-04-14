# AWS WAF Bot Control example: Exclude IP range from bot management<a name="waf-bot-control-example-scope-down-ip"></a>

If you want to exclude a subset of web traffic from AWS WAF Bot Control management, and you can identify that subset using a rule statement, then exclude it by adding a scope\-down statement to your Bot Control managed rule group statement\. 

The following rule performs normal Bot Control bot management on all web traffic except for web requests coming from a specific IP address range\.

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
          "IPSetReferenceStatement": {
            "ARN": "arn:aws:wafv2:us-east-1:123456789:regional/ipset/friendlyips/00000000-0000-0000-0000-000000000000"
          }
        }
      }
    }
  }
}
```