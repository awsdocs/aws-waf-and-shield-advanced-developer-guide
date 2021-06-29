# Managing rule group behavior in a web ACL<a name="web-acl-rule-group-settings"></a>

This section describes your options for modifying how you use a rule group in your web ACL\. This information applies to all rule group types\. After you add a rule group to a web ACL, you can override the actions of the individual rules in the rule group to count\. You can also override the rule group's resulting action to count, which has no effect on how the rules are evaluated inside the rule group\. 

For information about these options, see [Overriding the actions of a rule group or its rules](web-acl-rule-group-override-options.md)\.

## Setting rule actions to count in a rule group<a name="web-acl-rule-group-rule-to-count"></a>

For each rule group in a web ACL, you can override the contained rule's actions to count for some or all of the rules\. Rules that you alter like this are described as being *excluded rules* in the rule group\. If you have metrics enabled, you receive `COUNT` metrics for each excluded rule\. This change alters how the rules in the rule group are evaluated\.

**To set rule actions to count in a rule group**

1. After you've added your rule group to your web ACL, edit the web ACL\. 

1. In the web ACL page **Rules** tab, select the rule group, then choose **Edit**\. 

1. In the **Rules** section for the rule group, do one of the following: 
   + \(Option\) Turn on the **Set all rule actions to count** toggle\.
   + \(Option\) For each rule that you want to set to count, turn on the **Rule action** **Count** toggle\. 

1. Choose **Save rule**\.

The following example JSON listing shows a rule group declaration inside a web ACL that sets the rule actions to count for the rules `CategoryVerifiedSearchEngine` and `CategoryVerifiedSocialMedia`\. Through the API, in order to set all rule actions to count when you add a rule group to a web ACL, you list them all by name in `ExcludedRules` specification inside the rule group reference statement, as shown here\.

```
{
  "Name": "AWS-AWSBotControl-Example",
  "Priority": 5,
  "Statement": {
    "ManagedRuleGroupStatement": {
      "VendorName": "AWS",
      "Name": "AWSManagedRulesBotControlRuleSet",
      "ExcludedRules": [
        {
          "Name": "CategoryVerifiedSearchEngine"
        },
        {
          "Name": "CategoryVerifiedSocialMedia"
        }
      ]
    },
    "VisibilityConfig": {
      "SampledRequestsEnabled": true,
      "CloudWatchMetricsEnabled": true,
      "MetricName": "AWS-AWSBotControl-Example"
    }
  }
}
```

## Overriding a rule group's action to count<a name="web-acl-rule-group-action-override"></a>

You can override the action that a rule group returns to count, without altering how the rules in the rule group are configured or evaluated\. 

**To override the rule group's resulting action**

1. After you've added your rule group to your web ACL, edit the web ACL\. 

1. In the web ACL page **Rules** tab, select the rule group, then choose **Edit**\. 

1. Enable the option **Override rule group action**\. 

1. Choose **Save rule**\.

The following example JSON listing shows a rule group declaration inside a web ACL where the web ACL is configured to override the rule group action to count\. The override settings are in bold\. 

```
{
  "Name": "AWS-AWSBotControl-Example",
  "Priority": 5,
  "Statement": {
    "ManagedRuleGroupStatement": {
      "VendorName": "AWS",
      "Name": "AWSManagedRulesBotControlRuleSet"
    }
  },
  "OverrideAction": {
    "Count": {}
  },
  "VisibilityConfig": {
    "SampledRequestsEnabled": true,
    "CloudWatchMetricsEnabled": true,
    "MetricName": "AWS-AWSBotControl-Example"
  }
}
```