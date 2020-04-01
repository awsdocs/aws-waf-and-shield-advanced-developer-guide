# Working with managed rule groups<a name="waf-using-managed-rule-groups"></a>

This section provides guidance for accessing and managing managed rule groups\. 

**To retrieve a list of managed rule groups**
+ **Console** – During the process of creating a web ACL, on the **Add rules and rule groups** page, choose **Add managed rule groups**\. At the top level, the vendor names are listed\. Expand each vendor listing to see the list of managed rule groups\. When you add a managed rule group to your web ACL, the console lists it based on the naming scheme `<Vendor Name>-<Managed Rule Group Name>`\.
+ **API** – `ListAvailableManagedRuleGroups`
+ **CLI** – `aws wafv2 list-available-managed-rule-groups`

The API and CLI calls return a list of all managed rules that you can reference in the JSON model or through AWS CloudFormation\.

**To retrieve the list of rules in a managed rule group**
+ **Console** 

  1. Add the managed rule group into your web ACL and finish creating your web ACL\. For guidance, see [Creating a web ACL](web-acl-creating.md)\. 

  1. From the **Web ACLs** page, choose the web ACL you just created\. This takes you to the web ACL edit page\. 

  1. Choose **Rules**\. 

  1. Select the rule group you want to see a rules list for, then choose **Edit**\. AWS WAF shows the list of rules in the rule group\. 

     In this page, you can optionally put individual rules into count mode by selecting **Override rules action**\. 
+ **API** – `DescribeManagedRuleGroup`
+ **CLI** – `aws wafv2 describe-managed-rule-group --scope=REGIONAL --vendor-name=<vendor> --name=<managedrule_name>`

The API and CLI calls return a list of all rules in the managed rule group that you can reference in the JSON model or through AWS CloudFormation\.

**To add or modify managed rule groups using JSON**  
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

**To add or modify managed rule groups using AWS CloudFormation**  
You can reference and modify managed rule groups within a rule statement using the AWS CloudFormation template\. The following listing shows the AWS Managed Rules rule group, `AWSManagedRulesCommonRuleSet`, in AWS CloudFormation template\. The `ExcludedRules` specification lists rules whose actions are overridden to count only\.

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