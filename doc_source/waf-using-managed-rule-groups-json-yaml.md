# Example managed rule group configurations in JSON and YAML<a name="waf-using-managed-rule-groups-json-yaml"></a>

The API and CLI calls return a list of all rules in the managed rule group that you can reference in the JSON model or through AWS CloudFormation\.

**JSON**  
You can reference and modify managed rule groups within a rule statement using JSON\. The following listing shows the AWS Managed Rules rule group, `AWSManagedRulesCommonRuleSet`, in JSON format\. The RuleActionOverrides specification lists a rule whose action has been overridden to Count\. 

```
{
    "Name": "AWS-AWSManagedRulesCommonRuleSet",
    "Priority": 0,
    "Statement": {
      "ManagedRuleGroupStatement": {
        "VendorName": "AWS",
        "Name": "AWSManagedRulesCommonRuleSet",
        "RuleActionOverrides": [                                                                                                                                            
          {                                                                                                                                                                
            "ActionToUse": {                                                                                                                                              
              "Count": {}                                                                                                                                                
            },                                                                                                                                                            
            "Name": "NoUserAgent_HEADER"                                                                                                                                 
          }                                                                                                                                                                
        ],
        "ExcludedRules": []
      }
    },
    "OverrideAction": {
      "None": {}
    },
    "VisibilityConfig": {
      "SampledRequestsEnabled": true,
      "CloudWatchMetricsEnabled": true,
      "MetricName": "AWS-AWSManagedRulesCommonRuleSet"
    }
}
```

**YAML**  
You can reference and modify managed rule groups within a rule statement using the AWS CloudFormation YAML template\. The following listing shows the AWS Managed Rules rule group, `AWSManagedRulesCommonRuleSet`, in AWS CloudFormation template\. The RuleActionOverrides specification lists a rule whose action has been overridden to Count\. 

```
Name: AWS-AWSManagedRulesCommonRuleSet
Priority: 0
Statement:
  ManagedRuleGroupStatement:
    VendorName: AWS
    Name: AWSManagedRulesCommonRuleSet
    RuleActionOverrides:
    - ActionToUse:
        Count: {}
      Name: NoUserAgent_HEADER
    ExcludedRules: []
OverrideAction:
  None: {}
VisibilityConfig:
  SampledRequestsEnabled: true
  CloudWatchMetricsEnabled: true
  MetricName: AWS-AWSManagedRulesCommonRuleSet
```