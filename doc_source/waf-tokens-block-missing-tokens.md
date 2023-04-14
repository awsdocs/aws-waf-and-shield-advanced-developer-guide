# Blocking requests that don't have a valid token<a name="waf-tokens-block-missing-tokens"></a>

When you use the AWS Managed Rules rule groups `AWSManagedRulesATPRuleSet` and `AWSManagedRulesBotControlRuleSet`, the rule groups invoke the AWS WAF token management to evaluate the status of the AWS token in web requests and to label them accordingly\. 

**Note**  
Token labeling is only applied to web requests that you evaluate using one of these two managed rule groups\.

AWS WAF applies one of the following labels when it inspects a web request's token and challenge timestamp\. AWS WAF doesn't add labeling about the status of the CAPTCHA timestamp\. 
+ `awswaf:managed:token:accepted` – The request token is present and has an unexpired challenge timestamp\. 
+ `awswaf:managed:token:rejected` – The request token is present but is either corrupt or has an expired challenge timestamp\.
+ `awswaf:managed:token:absent` – The request doesn't have a token\.

The `AWSManagedRulesATPRuleSet` blocks requests with the `awswaf:managed:token:rejected` label\. The `AWSManagedRulesBotControlRuleSet` challenges clients after they send five requests without an accepted token\. For details about the rule groups, see [AWS WAF Fraud Control account takeover prevention \(ATP\) rule group](aws-managed-rule-groups-atp.md) and [AWS WAF Bot Control rule group](aws-managed-rule-groups-bot.md)\. 

The Bot Control rule group doesn't block a request with a rejected token, and neither rule group blocks an individual request that's missing its token\. If the request isn't blocked by some other rule in the rule group, it can exit the rule group evaluation and continue to be evaluated by the web ACL\. 

To block all requests that are missing their token or whose token is rejected, add a rule to run immediately after the managed rule group to capture and block requests that the rule group doesn't handle for you\. 

The following is an example JSON listing for a web ACL that uses the ATP managed rule group\. The web ACL has an added rule to capture the `awswaf:managed:token:absent` label and handle it\. The rule narrows its evaluation to web requests going to the login endpoint, to match the scope of the ATP rule group\. The added rule is listed in bold\. 

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
              "AWSManagedRulesATPRuleSet": {
                "LoginPath": "/web/login",
                "RequestInspection": {
                  "PayloadType": "JSON",
                  "UsernameField": {
                    "Identifier": "/form/username"
                  },
                  "PasswordField": {
                    "Identifier": "/form/password"
                  }
                },
                "ResponseInspection": {
                  "StatusCode": {
                    "SuccessCodes": [
                      200
                    ],
                    "FailureCodes": [
                      401,
                      403,
                      500
                    ]
                  }
                }
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
              "Statement": {
                "LabelMatchStatement": {
                  "Scope": "LABEL",
                  "Key": "awswaf:managed:token:absent"
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