# Managing rule group behavior in a web ACL<a name="waf-using-rule-groups"></a>

This section describes your options for modifying how you use a rule group in your web ACL\. This information applies to all rule group types\. 

## Overriding rule actions for a rule group<a name="rule-group-override"></a>

For each rule group in a web ACL, you can override the contained rule's actions by setting the override action for the rule group to **Override to count**\. If any of the rule actions in the group is set to block or allow, this override changes the behavior to only count\. For more information about this option, see [How AWS WAF processes a web ACL](web-acl-processing.md)\. 

To override the rule actions in a rule group, when you add the rule group to the web ACL, turn on the **Set rules action to count** toggle\. For more information on web ACL management, see [Managing and using a Web Access Control List \(Web ACL\)](web-acl.md)\. 

## Excluding a rule in a rule group<a name="rule-group-rule-exclusion"></a>

Excluding a single rule can help you troubleshoot false positives, which is when a rule group blocks traffic that you aren't expecting it to block\. You can identify the rule within the rule group that's doing the unexpected blocking, and then disable it by excluding it\. Excluding a rule overrides the action that's set on the rule to count\. If you have metrics enabled, you'll receive COUNT metrics for each excluded rule\. For more information about this option, see [How AWS WAF processes a web ACL](web-acl-processing.md)\. <a name="waf-managed-rule-group-exclude-rule-procedure"></a>

**To exclude a rule in a rule group**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. If not already enabled, enable AWS WAF logging\. For more information, see [Logging Web ACL traffic information](logging.md)\. Use the AWS WAF logs to identify the IDs of the rules that you want to exclude\. These are typically rules that are blocking legitimate requests\.

1. In the navigation pane, choose **Web ACLs**\.

1. Choose the web ACL that you want to edit\. This takes you to a page showing the web ACL overview, with other tabs available\. 
**Note**  
You must associate a rule group with the web ACL and save the web ACL before you can exclude a rule from that rule group\.

1. Choose the **Rules** tab\.

1. Select the rule group you want to see a rules list for, then choose **Edit**\. AWS WAF shows the list of rules in the rule group\. 

1. Select **Override rules action** for the rules you want to exclude from the rule group\. AWS WAF will count matching web requests for the rules that you exclude, and take no other action\. You receive count metrics for each rule in this state, if metrics are enabled for the rule group\. 