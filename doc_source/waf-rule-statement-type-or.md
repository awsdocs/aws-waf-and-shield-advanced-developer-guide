# `OR` rule statement<a name="waf-rule-statement-type-or"></a>

The `OR` rule statement combines nested statements with `OR` logic, so one of the nested statements must match for the `OR` statement to match\. This requires at least one nested statement\. 

For example, if you want to block requests that come from a specific country or that contain a specific query string, you could create an `OR` statement and nest in it a geographic match statement for the country and a string match statement for the query string\. 

If instead you want to block requests that *don't* come from a specific country or that contain a specific query string, you would modify the previous `OR` statement to nest the geographics match statement one level lower, inside a `NOT` statement\. This level of nesting requires you to use the JSON formatting, because the console supports only one level of nesting\.

**Nestable** – You can nest this statement type\. 

**WCUs** – Depends on the nested statements\.

**Where to find this**
+ **Rule builder** on the console – For **If a request**, choose **matches at least one of the statements \(OR\)**, and then fill in the nested statements\. 
+ **API statement** – `OrStatement`

**Examples**  
The following listing shows the use of `OR` to combine two other statements\. The `OR` statement is a match if either of the nested statements match\. 

```
{
  "Name": "neitherOfTwo",
  "Priority": 1,
  "Action": {
    "Block": {}
  },
  "VisibilityConfig": {
    "SampledRequestsEnabled": true,
    "CloudWatchMetricsEnabled": true,
    "MetricName": "neitherOfTwo"
  },
  "Statement": {
    "OrStatement": {
      "Statements": [
        {
          "GeoMatchStatement": {
            "CountryCodes": [
              "CA"
            ]
          }
        },
        {
          "IPSetReferenceStatement": {
            "ARN": "arn:aws:wafv2:us-east-1:111111111111:regional/ipset/test-ip-set-22222222/33333333-4444-5555-6666-777777777777"
          }
        }
      ]
    }
  }
}
```

Using the console rule visual editor, you can nest most nestable statements under a logical rule statement, but you can't use the visual editor to nest `OR` or `AND` statements\. To configure this type of nesting, you need to provide your rule statement in JSON\. For example, the following JSON rule listing includes an `OR` statement nested inside an `AND` statement\. 

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