# Example managed rule group configurations in JSON and YAML<a name="waf-using-managed-rule-groups-json-yaml"></a>

The API and CLI calls return a list of all rules in the managed rule group that you can reference in the JSON model or through AWS CloudFormation\.

**JSON**  
You can reference and modify managed rule groups within a rule statement using JSON\. The following listing shows the AWS Managed Rules rule group, `AWSManagedRulesCommonRuleSet`, in JSON format\. The `ExcludedRules` specification lists rules whose actions are overridden to count only\.

```
{
    "Name": "AWS-AWSManagedRulesCommonRuleSet",
    "Priority": 0,
    "Statement": {
      "ManagedRuleGroupStatement": {
        "VendorName": "AWS",
        "Name": "AWSManagedRulesCommonRuleSet",
        "ExcludedRules": [
          {
            "Name": "NoUserAgent_HEADER"
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
      "MetricName": "AWS-AWSManagedRulesCommonRuleSet"
    }
}
```

**YAML**  
You can reference and modify managed rule groups within a rule statement using the AWS CloudFormation YAML template\. The following listing shows the AWS Managed Rules rule group, `AWSManagedRulesCommonRuleSet`, in AWS CloudFormation template\. The `ExcludedRules` specification lists rules whose actions are overridden to count only\.

```
Description: WebACL With AMR
Resources:
  WebACLWithAMR:
    Type: AWS::WAFv2::WebACL
    Properties:
      Name: WebACLWithAMR
      Scope: REGIONAL
      Description: This is a demo
      DefaultAction: 
        Block: {}
      VisibilityConfig:
        SampledRequestsEnabled: true
        CloudWatchMetricsEnabled: true
        MetricName: MetricForWebACLWithAMR
      Tags:
        - Key: sampleapple
          Value: sampleorange
      Rules: 
        - Name: AWS-AWSManagedRulesCommonRuleSet
          Priority: 0
          OverrideAction:
            None: {}
          VisibilityConfig:
            SampledRequestsEnabled: true
            CloudWatchMetricsEnabled: true
            MetricName: MetricForAMRCRS
          Statement:
            ManagedRuleGroupStatement:
              VendorName: AWS
              Name: AWSManagedRulesCommonRuleSet
              ExcludedRules:
                - Name: NoUserAgent_HEADER
```