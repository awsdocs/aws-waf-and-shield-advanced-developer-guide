# Step 3: Create a Rule Group<a name="get-started-fms-create-rule-group"></a>

A rule group is a set of rules that defines what actions to take when a particular set of conditions is met\. You can purchase managed rule groups from AWS Marketplace, or you can create your own rule group\.

To purchase a managed rule group from AWS Marketplace, see [AWS Marketplace Rule Groups](waf-managed-rule-groups.md)\.

To create your own rule group, perform the following procedure\.<a name="get-started-fms-create-rule-group-procedure"></a>

**To create a rule group \(console\)**

1. Sign in to the AWS Management Console using the AWS Firewall Manager administrator account that you set up in the prerequisites, and then open the Firewall Manager console at [https://console\.aws\.amazon\.com/waf/fms](https://console.aws.amazon.com/waf/fms)\. 

1. In the navigation pane, choose **Security policies**\. 

1. If you have not met the prerequisites, the console displays instructions about how to fix any issues\. Follow the instructions, and then begin this step \(create a rule group\) again\. If you have met the prerequisites, choose **Close**\. 

1. Choose **Create policy**\.

1. Choose **Create an AWS Firewall Manager policy and add a new rule group**\.

1. Choose an AWS Region, and then choose **Next**\.

1. Because you already created rules, you don't need to create conditions\. Choose **Next**\.

1. Because you already created rules, you don't need to create rules\. Choose **Next**\.

1. Choose **Create rule group**\.

1. For **Name**, enter a friendly name\. 

1. Enter a name for the CloudWatch metric that AWS WAF will create and will associate with the rule group\. The name can contain only alphanumeric characters \(A\-Z, a\-z, 0\-9\) or the following special characters: \_\-\!"\#`\+\*\},\./\. It can't contain white space\.

1. Select a rule, and then choose **Add rule**\. Repeat adding rules until you have added all the rules that you want to the rule group\.

1. A rule group has two possible actions: **Block** and **Count**\. If you want to test the rule group, set the action to **Count**\. This action overrides any *block* action specified by individual rules contained in the group\. That is, if the rule group's action is set to **Count**, requests are only counted and not blocked\. Conversely, if you set the rule group's action to **Block**, actions of the individual rules in the group are used\. For this tutorial, choose **Count**\.

1. Choose **Create**\.

You are now ready to go to [Step 4: Create and Apply an AWS Firewall Manager AWS WAF Policy](get-started-fms-create-security-policy.md)\.