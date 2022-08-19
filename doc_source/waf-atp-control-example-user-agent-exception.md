# ATP example: Custom handling for missing and compromised credentials<a name="waf-atp-control-example-user-agent-exception"></a>

By default, the credentials checks that are performed by the rule group `AWSManagedRulesATPRuleSet` handle web requests as follows: 
+ **Missing credentials** – Label and block request\.
+ **Compromised credentials** – Label request but don't block or count it\.

For details about the rule group and rule behavior, see [AWS WAF Fraud Control account takeover prevention \(ATP\) rule group](aws-managed-rule-groups-atp.md)\.

You can add custom handling for web requests that have missing or compromised credentials by doing the following: 
+ **Exclude the `MissingCredential` rule** – When you exclude this blocking rule, it only counts and labels matching requests\.
+ **Add a label match rule with custom handling** – Configure your rule to match against both of the ATP labels and to perform your custom handling\. For example, you might redirect the customer to your sign\-up page\.

The following rule shows the ATP managed rule group from the prior example, with the `MissingCredential` rule excluded\. This exclusion causes the rule to apply its label to matching requests, and then only count the requests, instead of blocking them\. 

```
"Rules": [
    {
        "Priority": 1,
        "OverrideAction": {
            "None": {}
        },
        "VisibilityConfig": {
            "SampledRequestsEnabled": true,
            "CloudWatchMetricsEnabled": true,
            "MetricName": "AccountTakeOverValidationRule"
        },
        "Name": "DetectCompromisedUserCredentials",
        "Statement": {
            "ManagedRuleGroupStatement": {
                "ManagedRuleGroupConfigs": [
                    {
                        "UsernameField": {
                           "Identifier": "/form/username"
                        }
                    },
                    {
                        "PasswordField": {
                            "Identifier": "/form/password"
                        }
                    },
                    {
                        "PayloadType": "JSON"
                    },
                    {
                        "LoginPath": "/web/login"
                    }
                ],
                "VendorName": "AWS",
                "Name": "AWSManagedRulesATPRuleSet",
                "ExcludedRules": [
                  {
                    "Name": "MissingCredential"
                  }
                ]
            }
        }
    }
],
```

With this configuration, when this rule group evaluates any web request that has missing or compromised credentials, it will label the request, but not block it\. 

The following rule has a higher numeric priority than the preceding rule group, so that it's evaluated after the rule group evaluation\. It's configured to match either of the credentials labels and to send a custom response for matching requests\. 

```
"Name": "redirectToSignup",
      "Priority": 10,
      "Statement": {
        "OrStatement": {
          "Statements": [
            {
              "LabelMatchStatement": {
                "Scope": "LABEL",
                "Key": "awswaf:managed:aws:atp:signal:missing_credential"
              }
            },
            {
              "LabelMatchStatement": {
                "Scope": "LABEL",
                "Key": "awswaf:managed:aws:atp:signal:credential_compromised"
              }
            }
          ]
        }
      },
      "Action": {
        "Block": {
          "CustomResponse": {
             your custom response settings 
          }
        }
      },
      "VisibilityConfig": {
        "SampledRequestsEnabled": true,
        "CloudWatchMetricsEnabled": true,
        "MetricName": "redirectToSignup"
      }
```