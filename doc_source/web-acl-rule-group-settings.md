# Managing rule group behavior in a web ACL<a name="web-acl-rule-group-settings"></a>

This section describes your options for modifying how you use a rule group in your web ACL\. This information applies to all rule group types\. After you add a rule group to a web ACL, you can override the actions of the individual rules in the rule group to Count or to any other valid rule action setting\. You can also override the rule group's resulting action to Count, which has no effect on how the rules are evaluated inside the rule group\. 

For information about these options, see [Action overrides in rule groups](web-acl-rule-group-override-options.md)\.

## Overriding rule actions in a rule group<a name="web-acl-rule-group-rule-action-override"></a>

For each rule group in a web ACL, you can override the contained rule's actions for some or all of the rules\. 

The most common use case for this is overriding the rule actions to Count to test new or updated rules\. If you have metrics enabled, you receive count metrics for each rule that you override to count\. For more information about testing, see [Testing and tuning your AWS WAF protections](web-acl-testing.md)\.

**To override rule actions in a rule group**

You can make these changes when you're adding the rule group to the web ACL or later\. These instructions are for a rule group that has already been added to the web ACL\. See the additional information about this option at [Rule action overrides](web-acl-rule-group-override-options.md#web-acl-rule-group-override-options-rules)\.

1. Edit the web ACL\. 

1. In the web ACL page **Rules** tab, select the rule group, then choose **Edit**\. 

1. In the **Rules** section for the rule group, manage the action settings as needed\. 
   + **All rules** – To set an override action for all rules in the rule group, open the **Override all rule actions** dropdown and select the override action\. To remove the overrides for all rules, select **Remove all overrides**\. 
   + **Single rule** – To set an override action for a single rule, open the rule's dropdown and select the override action\. To remove an override for a rule, open the rule's dropdown and select **Remove override**\.

1. When you are finished making your changes, choose **Save rule**\. The rule action and override action settings are listed in the rule group page\. 

The following example JSON listing shows a rule group declaration inside a web ACL that overrides the rule actions to Count for the rules `CategoryVerifiedSearchEngine` and `CategoryVerifiedSocialMedia`\. In the JSON, you override all rule actions by providing a `RuleActionOverrides` entry for each individual rule\.

```
{
    "Name": "AWS-AWSBotControl-Example",
   "Priority": 5, 
   "Statement": {
    "ManagedRuleGroupStatement": {
        "VendorName": "AWS",
        "Name": "AWSManagedRulesBotControlRuleSet",
        "RuleActionOverrides": [
          {
            "ActionToUse": {
              "Count": {}
            },
            "Name": "CategoryVerifiedSearchEngine"
          },
          {
            "ActionToUse": {
              "Count": {}
            },
            "Name": "CategoryVerifiedSocialMedia"
          }
        ],
        "ExcludedRules": []
    },
   "VisibilityConfig": {
       "SampledRequestsEnabled": true,
       "CloudWatchMetricsEnabled": true,
       "MetricName": "AWS-AWSBotControl-Example"
   }
}
```

## Overriding a rule group's evaluation result to Count<a name="web-acl-rule-group-action-override"></a>

You can override the action that results from a rule group evaluation, without altering how the rules in the rule group are configured or evaluated\. This option is not commonly used\. If any rule in the rule group results in a match, this override sets the resulting action from the rule group to Count\.

You can override the rule group's resulting action in the web ACL when you add or edit the rule group\. In the console, open the rule group's **Override rule group action \- optional** pane and enable the override\. In the JSON set `OverrideAction` in the rule group statement, as shown in the following example listing: 

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