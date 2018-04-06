# Adding and Deleting Rules from a Rule Group<a name="rule-group-editing"></a>

You can add or delete rules in a rule group\.

Deleting a rule from the rule group does not delete the rule itself\. It only removes the rule from the rule group\.<a name="rule-group-editing-procedure"></a>

**To add or delete rules in a rule group \(console\)**

1. Sign in to the AWS Management Console using the Firewall Manager administrator account that you set up in the prerequisites, and then open the Firewall Manager console at https://console\.aws\.amazon\.com/waf/fms\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [Step 2: Set the AWS Firewall Manager Administrator Account](enable-integration.md)\.

1. In the navigation pane, choose **Rule groups**\.

1. Choose the rule group that you want to edit\.

1. Choose **Edit rule group**\.

1. To add rules, perform the following steps:

   1. Select a rule, and then choose **Add another rule**\. Repeat to add more rules to the rule group\. 
**Note**  
You cannot add rate\-based rules to rule group\.

   1. Choose **Update**\.

1. To delete rules, perform the following steps:

   1. Choose the **X** next to the rule to delete\. Repeat to delete more rules from the rule group\.

   1. Choose **Update**\.