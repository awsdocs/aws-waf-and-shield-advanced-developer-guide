# Step 2: Create and apply an AWS Firewall Manager AWS WAF policy<a name="get-started-fms-create-security-policy"></a>

A Firewall Manager AWS WAF policy contains the rule groups that you want to apply to your resources\. Firewall Manager creates a Firewall Manager web ACL in each account where you apply the policy\. The individual account managers can add rules and rule groups to the resulting web ACL, in addition to the rule groups that you define here\. For information about Firewall Manager AWS WAF policies, see [AWS WAF policies](waf-policies.md)\.

**To create a Firewall Manager AWS WAF policy \(console\)**

1. Sign in to the AWS Management Console using the Firewall Manager administrator account that you set up in the prerequisites, and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [Step 2: Set the AWS Firewall Manager administrator account](enable-integration.md)\.

1. In the navigation pane, choose **Security policies**\.

1. Choose **Create policy**\.

1. For **Policy type**, choose **AWS WAF**\. 

1. For **Region**, choose an AWS Region\. To protect Amazon CloudFront distributions, choose **Global**\.

   To protect resources in multiple Regions \(other than CloudFront distributions\), you must create separate Firewall Manager policies for each Region\.

1. Choose **Next**\.

1. For **Policy name**, enter a descriptive name\. Firewall Manager includes the policy name in the names of the web ACLs that it creates\. The web ACL names begin with `FMManagedWebACLV2` followed by the policy name that you enter here\. 

1. Under **Policy rules**, for **First rule groups**, choose **Add rule groups**\. Expand the **AWS managed rule groups**\. For **Core rule set**, toggle **Add to web ACL**\. For **AWS Known bad inputs**, toggle **Add to web ACL**\. Choose **Add rules**\.

   For **Last rule groups**, choose **Add rule groups**\. Expand the **AWS managed rule groups** and for the **Amazon IP reputation list**, toggle **Add to web ACL**\. Choose **Add rules**\.

   Under **First rule groups**, select **Core rule set** and choose **Move down**\. AWS WAF evaluates web requests against the **AWS Known bad inputs** rule group before it evaluates against the **Core rule set**\. 
**Note**  
You can also create your own AWS WAF rule groups if you want, using the AWS WAF console\. Any rule groups that you create show up under **Your rule groups** in the **Describe policy : Add rule groups page**\. 

1. Leave the default action for the web ACL at **Allow**\. 

1. Leave the **Policy action** at the default, to not automatically remediate noncompliant resources\. You can change the option later\. 

1. Choose **Next**\.

1. For **Policy scope**, you provide the settings for the accounts, resource types, and tagging that identify the resources you want to apply the policy to\. For this tutorial, leave the **AWS accounts** and **Resources** settings, and choose one or more resource types\.

1. Choose **Next**\.

1. For **Policy tags**, you can add any identifying tags that you want for the Firewall Manager AWS WAF policy\. For more information about tags, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\. For this tutorial, you can leave this alone\.

1. Choose **Next**\.

1. Review the new policy\. You can make changes by choosing **Edit** in the area that you want to change\. This returns you to the corresponding step in the creation wizard\. When you are satisfied with the policy, choose **Create policy**\.