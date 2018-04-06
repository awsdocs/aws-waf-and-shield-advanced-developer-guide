# Creating a Rule Group<a name="create-rule-group"></a>

When you create a rule group to use with AWS Firewall Manager, you specify which rules to add to the group\.<a name="create-rule-group-procedure"></a>

**To create a rule group \(console\)**

1. Sign in to the AWS Management Console using the AWS Firewall Manager administrator account that you set up in the prerequisites, and then open the Firewall Manager console at https://console\.aws\.amazon\.com/waf/fms\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [Step 2: Set the AWS Firewall Manager Administrator Account](enable-integration.md)\.

1. In the navigation pane, choose **Rule groups**\.

1. Choose **Create rule group**\.

1. If you have already created the rules that you want to add to the rule group, choose **Use existing rules for this rule group **\. If you want to create new rules to add to the rule group, choose **Create rules and conditions for this rule group**\.
**Note**  
You cannot add rate\-based rules to rule group\.

1. Choose **Next**\.

1. If you are creating new rules, follow the steps to first create conditions and then rules\. For more information, see [Working with conditions](web-acl-create-condition.md) and [Working with Rules](web-acl-rules.md)\. If you are using existing rules, go to the next step\.

1. Type a rule group name\.

1. Select a rule, and then choose **Add rule**\. Repeat to add more rules to the rule group\.

1. A rule group has two possible actions: **Block** and **Count**\. If you want to test the rule group, set the action to **Count**\. This action overrides any *block* action specified by individual rules contained in the group\. That is, if the rule group's action is set to **Count**, requests are only counted and not blocked\. Conversely, if you set the rule group's action to **Block**, actions of the individual rules in the group are used\. For each rule, select the appropriate option\.

1. Choose **Create**\.