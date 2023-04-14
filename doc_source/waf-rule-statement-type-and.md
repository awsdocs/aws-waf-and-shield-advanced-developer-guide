# AND rule statement<a name="waf-rule-statement-type-and"></a>

The AND rule statement combines nested statements with a logical AND operation, so all nested statements must match for the AND statement to match\. This requires at least one nested statement\. 

**Nestable** – You can nest this statement type\. 

**WCUs** – Depends on the nested statements\.

**Where to find this rule statement**
+ **Rule builder** on the console – For **If a request**, choose **matches all the statements \(AND\)**, and then fill in the nested statements\. 
+ **API** – [AndStatement](https://docs.aws.amazon.com/waf/latest/APIReference/API_AndStatement.html)

**Examples**  
The following listing shows the use of AND and NOT logical rule statements to eliminate false positives from the matches for an SQL injection attack statement\. For this example, suppose we can write a single byte match statement to match the requests that are resulting in false positives\. 

The AND statement matches for requests that do not match the byte match statement and that do match the SQL injection attack statement\. 

```
{
      "Name": "SQLiExcludeFalsePositives",
      "Priority": 0,
      "Statement": {
        "AndStatement": {
          "Statements": [
            {
              "NotStatement": {
                "Statement": {
                  "ByteMatchStatement": {
                    "SearchString": "string identifying a false positive",
                    "FieldToMatch": {
                      "Body": {
                        "OversizeHandling": "MATCH"
                      }
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
            },
            {
              "SqliMatchStatement": {
                "FieldToMatch": {
                  "Body": {
                    "OversizeHandling": "MATCH"
                  }
                },
                "TextTransformations": [
                  {
                    "Priority": 0,
                    "Type": "NONE"
                  }
                ]
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
        "MetricName": "SQLiExcludeFalsePositives"
      }
    }
```

Using the console rule visual editor, you can nest a non\-logical statement or a NOT statement under an OR or AND statement\. The nesting of the NOT statement is shown in the prior example\. 

Using the console rule visual editor, you can nest most nestable statements under a logical rule statement, such as the one shown in the prior example\. You can't use the visual editor to nest OR or AND statements\. To configure this type of nesting, you need to provide your rule statement in JSON\. For example, the following JSON rule listing includes an OR statement nested inside an AND statement\. 

```
{
  "Name": "match_rule",
  "Priority": 0,
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
        },
        {
          "OrStatement": {
            "Statements": [
              {
                "GeoMatchStatement": {
                  "CountryCodes": [
                    "JM",
                    "JP"
                  ]
                }
              },
              {
                "ByteMatchStatement": {
                  "SearchString": "JCountryString",
                  "FieldToMatch": {
                    "Body": {}
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
            ]
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