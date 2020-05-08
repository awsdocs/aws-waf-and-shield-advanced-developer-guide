# Step 3: Create a rule group<a name="classic-get-started-fms-create-rule-group"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

A rule group is a set of rules that defines what actions to take when a particular set of conditions is met\. You can use managed rule groups from AWS Marketplace, and you can create your own rule groups\. For information about managed rule groups, see [AWS marketplace rule groups](classic-waf-managed-rule-groups.md)\.

To create your own rule group, perform the following procedure\.<a name="classic-get-started-fms-create-rule-group-procedure"></a>

**To create a rule group \(console\)**

1. Sign in to the AWS Management Console using the AWS Firewall Manager administrator account that you set up in the prerequisites, and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 

1. In the navigation pane, choose **Security policies**\. 

1. If you have not met the prerequisites, the console displays instructions about how to fix any issues\. Follow the instructions, and then begin this step \(create a rule group\) again\. If you have met the prerequisites, choose **Close**\. 

1. Choose **Create policy**\.

   For **Policy type**, choose **AWS WAF Classic**\. 

1. Choose **Create an AWS Firewall Manager policy and add a new rule group**\.

1. Choose an AWS Region, and then choose **Next**\.

1. Because you already created rules, you don't need to create conditions\. Choose **Next**\.

1. Because you already created rules, you don't need to create rules\. Choose **Next**\.

1. Choose **Create rule group**\.

1. For **Name**, enter a friendly name\. 

1. Enter a name for the CloudWatch metric that AWS WAF Classic will create and will associate with the rule group\. The name can contain only alphanumeric characters \(A\-Z, a\-z, 0\-9\) or the following special characters: \_\-\!"\#`\+\*\},\./\. It can't contain white space\.

1. Select a rule, and then choose **Add rule**\. A rule has an action setting that allows you to choose whether to allow, block, or count requests that match the rule's conditions\. For this tutorial, choose **Count**\. Repeat adding rules until you have added all the rules that you want to the rule group\.

1. Choose **Create**\.

You are now ready to go to [Step 4: Create and apply an AWS Firewall Manager AWS WAF Classic policy](classic-get-started-fms-create-security-policy.md)\.