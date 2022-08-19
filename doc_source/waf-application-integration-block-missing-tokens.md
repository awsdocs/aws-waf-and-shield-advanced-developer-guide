# Blocking login requests that don't have a token<a name="waf-application-integration-block-missing-tokens"></a>

The AWS Managed Rules rule group `AWSManagedRulesATPRuleSet` allows requests with valid tokens and blocks requests with invalid tokens when you use it with the application integration SDKs\. For details about the rule group, see [AWS WAF Fraud Control account takeover prevention \(ATP\) rule group](aws-managed-rule-groups-atp.md)\.

The rule group doesn't block or label requests that are missing tokens\. A request that's missing its token gets evaluated as follows by the rule group's token validation functionality: 

1. The `TokenRejected` rule results in no match, because there's no token to inspect\. It doesn't block the request, and it does *not* apply the label `awswaf:managed:token:rejected` to the request\. 

1. The token validation service doesn't apply the label `awswaf:managed:token:accepted` to the request\. 

Unless the request is blocked by some other rule in the rule group, it will exit the rule group evaluation without any token inspection labels, and continue to be evaluated by the web ACL\. 

To block requests to your login endpoint that are missing their token, add a rule to run immediately after the ATP managed rule group that blocks requests to the login endpoint if they don't have the `awswaf:managed:token:accepted` label\. 

The following is an example JSON listing for a web ACL that has the managed rule group and the added rule\. The added rule is listed in bold\. 

```
{
  "Name": "exampleWebACL",
  "Id": "55555555-6666-7777-8888-999999999999",
  "ARN": "arn:aws:wafv2:us-east-1:111111111111:regional/webacl/exampleWebACL/55555555-4444-3333-2222-111111111111",
  "DefaultAction": {
    "Allow": {}
  },
  "Description": "",
  "Rules": [
    {
      "Name": "AWS-AWSManagedRulesATPRuleSet",
      "Priority": 1,
      "Statement": {
        "ManagedRuleGroupStatement": {
          "VendorName": "AWS",
          "Name": "AWSManagedRulesATPRuleSet",
          "ManagedRuleGroupConfigs": [
            {
              "LoginPath": "/web/login"
            },
            {
              "PayloadType": "JSON"
            },
            {
              "UsernameField": {
                "Identifier": "/form/username"
              }
            },
            {
              "PasswordField": {
                "Identifier": "/form/password"
              }
            }
          ]
        }
      },
      "OverrideAction": {
        "None": {}
      },
      "VisibilityConfig": {
        "SampledRequestsEnabled": true,
        "CloudWatchMetricsEnabled": true,
        "MetricName": "AWS-AWSManagedRulesATPRuleSet"
      }
    },
    {
      "Name": "RequireTokenForLogins",
      "Priority": 2,
      "Statement": {
        "AndStatement": {
          "Statements": [
            {
              "NotStatement": {
                "Statement": {
                  "LabelMatchStatement": {
                    "Scope": "LABEL",
                    "Key": "awswaf:managed:token:accepted"
                  }
                }
              }
            },
            {
              "ByteMatchStatement": {
                "SearchString": "/web/login",
                "FieldToMatch": {
                  "UriPath": {}
                },
                "TextTransformations": [
                  {
                    "Priority": 0,
                    "Type": "NONE"
                 }
                ],
                "PositionalConstraint": "STARTS_WITH"
              }
            },
            {
              "ByteMatchStatement": {
                "SearchString": "POST",
                "FieldToMatch": {
                  "Method": {}
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
          ]
        }
      },
      "Action": {
        "Block": {}
      },
      "VisibilityConfig": {
        "SampledRequestsEnabled": true,
        "CloudWatchMetricsEnabled": true,
        "MetricName": "RequireTokenForLogins"
      } 
    }
  ],
  "VisibilityConfig": {
    "SampledRequestsEnabled": true,
    "CloudWatchMetricsEnabled": true,
    "MetricName": "exampleWebACL"
  },
  "Capacity": 51,
  "ManagedByFirewallManager": false,
  "LabelNamespace": "awswaf:111111111111:webacl:exampleWebACL:"
}
```