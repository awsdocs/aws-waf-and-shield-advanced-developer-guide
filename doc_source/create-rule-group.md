# Creating a Rule Group<a name="create-rule-group"></a>

When you create a rule group to use with AWS Firewall Manager, you specify which rules to add to the group\.<a name="create-rule-group-procedure"></a>

**To create a rule group \(console\)**

1. Sign in to the AWS Management Console using the AWS Firewall Manager administrator account that you set up in the prerequisites, and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [Step 2: Set the AWS Firewall Manager Administrator Account](enable-integration.md)\.

1. In the navigation pane, choose **Rule groups**\.

1. Choose **Create rule group**\.
**Note**  
You can't add rate\-based rules to a rule group\.

1. If you have already created the rules that you want to add to the rule group, choose **Use existing rules for this rule group **\. If you want to create new rules to add to the rule group, choose **Create rules and conditions for this rule group**\. 

1. Choose **Next**\.

1. If you chose to create rules, follow the steps to create conditions and then rules\. For more information, see [Working with Conditions](web-acl-create-condition.md) and [Working with Rules](web-acl-rules.md)\. When all of the rules you need have been created, go to the next step\.

1. Type a rule group name\.

1. To add a rule to the rule group, select a rule then choose **Add rule**\. Choose whether to allow, block, or count requests that match the rule's conditions\. For more information on the choices, see [How AWS WAF Works](how-aws-waf-works.md)\. 

1. When you are finished adding rules, choose **Create**\.

You can test your rule group by adding it to an AWS WAF WebACL and setting the WebACL action to **Override to Count**\. This action overrides any action that you choose for the rules contained in the group, and only counts matching requests\. For more information, see [Creating a Web ACL](web-acl-creating.md)\.