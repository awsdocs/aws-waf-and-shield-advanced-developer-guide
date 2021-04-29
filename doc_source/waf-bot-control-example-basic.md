# AWS WAF Bot Control example: Simple configuration<a name="waf-bot-control-example-basic"></a>

The following JSON listing shows an example web ACL with an AWS WAF Bot Control managed rule group\. Note the visibility configuration, which allows you to get sampling and metrics for monitoring purposes\. 

```
{
  "Name": "Bot-Beta-WebACL",
  "Id": "...",
  "ARN": "...",
  "DefaultAction": {
    "Allow": {}
  },
  "Description": "Bot-Beta-WebACL",
  "Rules": [
    {
      ...
    },
    {
       "Name": "AWS-AWSBotControl-Example",
       "Priority": 5,
       "Statement": {
          "ManagedRuleGroupStatement": {
             "VendorName": "AWS",
             "Name": "AWSManagedRulesBotControlRuleSet"
          },
          "VisibilityConfig": {
             "SampledRequestsEnabled": true,
             "CloudWatchMetricsEnabled": true,
             "MetricName": "AWS-AWSBotControl-Example"
           }
        }
    ],
    "VisibilityConfig": {
      ...
    },
    "Capacity": 1496,
    "ManagedByFirewallManager": false
}
```