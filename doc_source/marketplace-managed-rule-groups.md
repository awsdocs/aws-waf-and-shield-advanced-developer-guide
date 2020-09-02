# AWS Marketplace managed rule groups<a name="marketplace-managed-rule-groups"></a>

AWS Marketplace managed rule groups are available by subscription through the AWS Marketplace console at [AWS Marketplace](https://aws.amazon.com/marketplace)\. After you subscribe to a AWS Marketplace managed rule group, you can use it in AWS WAF\. To use an AWS Marketplace rule group in an AWS Firewall Manager AWS WAF policy, each account in your organization must subscribe to it\. 

**AWS Marketplace Rule Group Pricing**  
AWS Marketplace rule groups are available with no long\-term contracts, and no minimum commitments\. When you subscribe to a rule group, you are charged a monthly fee \(prorated hourly\) and ongoing request fees based on volume\. For more information, see [AWS WAF Pricing](https://aws.amazon.com/waf/pricing/) and the description for each AWS Marketplace rule group at [AWS Marketplace](https://aws.amazon.com/marketplace)\.

## Subscribing to AWS Marketplace managed rule groups<a name="marketplace-managed-rule-groups-subscribing"></a>

You can subscribe to and unsubscribe from AWS Marketplace rule groups on the AWS WAF console\. If you need to, you can exclude specific rules in a managed rule group when you add it to a web ACL\.

**Important**  
To use an AWS Marketplace rule group in an AWS Firewall Manager policy, each account in your organization must first subscribe to that rule group\. 

**To subscribe to an AWS Marketplace managed rule group**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **AWS Marketplace**\.

1. In the **Available marketplace products** section, choose the name of a rule group to view the details and pricing information\.

1. If you want to subscribe to the rule group, choose **Continue**\.
**Note**  
If you don't want to subscribe to this rule group, simply close this page in your browser\.

1. Choose **Set up your account**\.

1. Add the rule group to a web ACL, similar to how you add an individual rule\. For more information, see [Creating a web ACL](web-acl-creating.md) or [Editing a Web ACL](web-acl-editing.md)\.
**Note**  
When adding a rule group to a web ACL, you can override the actions of all rules in the rule group to `COUNT` only\. For more information, see [Overriding rule actions for a rule group](waf-using-rule-groups.md#rule-group-override)\.

After you're subscribed to an AWS Marketplace rule group, you use it in your web ACLs as you do other managed rule groups\. For information, see [Creating a web ACL](web-acl-creating.md)\.

## Unsubscribing from AWS Marketplace managed rule groups<a name="marketplace-managed-rule-groups-unsubscribing"></a>

You can unsubscribe from AWS Marketplace rule groups on the AWS WAF console\. 

**Important**  
To stop the subscription charges for an AWS Marketplace managed rule group, you must remove it from all web ACLs in AWS WAF and in any Firewall Manager AWS WAF policies, in addition to unsubscribing from it\. If you unsubscribe from an AWS Marketplace managed rule group but don't remove it from your web ACLs, you will continue to be charged for the subscription\. 

**To unsubscribe from an AWS Marketplace managed rule group**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. Remove the rule group from all web ACLs\. For more information, see [Editing a Web ACL](web-acl-editing.md)\.

1. In the navigation pane, choose **AWS Marketplace**\.

1. Choose **Manage your subscriptions**\.

1. Choose **Cancel subscription** next to the name of the rule group that you want to unsubscribe from\.

1. Choose **Yes, cancel subscription**\.

## Troubleshooting AWS Marketplace rule groups<a name="waf-managed-rule-group-troubleshooting"></a>

If you find that an AWS Marketplace rule group is blocking legitimate traffic, you can troubleshoot the problem by performing the following steps\.<a name="waf-managed-rule-group-troubleshooting-procedure"></a>

**To troubleshoot an AWS Marketplace rule group**

1. Exclude the specific rules that are blocking legitimate traffic\. You can identify which rules are blocking which requests using either the AWS WAF sampled requests or AWS WAF logs\. You can identify the rules by looking at the `ruleGroupId` field in the log or the `RuleWithinRuleGroup` in the sampled request\. You can identify the rule in the pattern `<Seller Name>#<RuleGroup Name>#<Rule Name>`\. 

1. If excluding specific rules does not solve the problem, you can change the action for the AWS Marketplace rule group from **No override** to **Override to count**\. This allows the web request to pass through, regardless of the individual rule actions within the rule group\. This also provides you with Amazon CloudWatch metrics for the rule group\.

1. After setting the AWS Marketplace rule group action to **Override to count**, contact the rule group provider‘s customer support team to further troubleshoot the issue\. For contact information, see the rule group listing on the product listing pages on AWS Marketplace\.

### Contacting AWS support<a name="waf-managed-rule-group-troubleshooting-support"></a>

For problems with AWS WAF or a rule group that is managed by AWS, contact AWS Support\. For problems with a rule group that is managed by an AWS AWS Marketplace seller, contact the vendor's customer support team\. To find vendor contact information, see the vendors’s listing on AWS Marketplace\.