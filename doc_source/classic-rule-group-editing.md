# Adding and deleting rules from an AWS WAF Classic rule group<a name="classic-rule-group-editing"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

You can add or delete rules in an AWS WAF Classic rule group\.

Deleting a rule from the rule group does not delete the rule itself\. It only removes the rule from the rule group\.<a name="classic-rule-group-editing-procedure"></a>

**To add or delete rules in a rule group \(console\)**

1. Sign in to the AWS Management Console using the AWS Firewall Manager administrator account that you set up in the prerequisites, and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [Step 2: Set the AWS Firewall Manager administrator account](enable-integration.md)\.

1. In the navigation pane, choose **Switch to AWS WAF Classic**\.

1. In the AWS WAF Classic navigation pane, choose **Rule groups**\.

1. Choose the rule group that you want to edit\.

1. Choose **Edit rule group**\.

1. To add rules, perform the following steps:

   1. Select a rule, and then choose **Add rule to rule group**\. Choose whether to allow, block, or count requests that match the rule's conditions\. For more information on the choices, see [How AWS WAF Classic works](classic-how-aws-waf-works.md)\. Repeat to add more rules to the rule group\. 
**Note**  
You cannot add rate\-based rules to rule group\.

   1. Choose **Update**\.

1. To delete rules, perform the following steps:

   1. Choose the **X** next to the rule to delete\. Repeat to delete more rules from the rule group\.

   1. Choose **Update**\.