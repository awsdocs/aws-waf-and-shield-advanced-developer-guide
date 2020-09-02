# Step 4: Create and apply an AWS Firewall Manager AWS WAF Classic policy<a name="classic-get-started-fms-create-security-policy"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

After you create the rule group, you create an AWS Firewall Manager AWS WAF policy\. A Firewall Manager AWS WAF policy contains the rule group that you want to apply to your resources\.<a name="classic-get-started-fms-create-security-policy-procedure"></a>

**To create a Firewall Manager AWS WAF policy \(console\)**

1. After you create the rule group \(the last step in the preceding procedure, [Step 3: Create a rule group](classic-get-started-fms-create-rule-group.md)\), the console displays the **Rule group summary** page\. Choose **Next**\.

1. For **Name**, enter a friendly name\. 

1. For **Policy type**, choose **WAF**\. 

1. For **Region**, choose an AWS Region\. To protect Amazon CloudFront resources, choose **Global**\.

   To protect resources in multiple regions \(other than CloudFront resources\), you must create separate Firewall Manager policies for each Region\.

1. Select a rule group to add, and then choose **Add rule group**\. 

1. A policy has two possible actions: **Action set by rule group** and **Count**\. If you want to test the policy and rule group, set the action to **Count**\. This action overrides any *block* action specified by the rule group contained in the policy\. That is, if the policy's action is set to **Count**, those requests are only counted and not blocked\. Conversely, if you set the policy's action to **Action set by rule group**, actions of the rule group in the policy are used\. For this tutorial, choose **Count**\.

1. Choose **Next**\.

1. If you want to include only specific accounts in the policy, or alternatively exclude specific accounts from the policy, select **Select accounts to include/exclude from this policy \(optional\)**\. Choose either **Include only these accounts in this policy** or **Exclude these accounts from this policy**\. You can choose only one option\. Choose **Add**\. Select the account numbers to include or exclude, and then choose **OK**\. 
**Note**  
If you don't select this option, Firewall Manager applies a policy to all accounts in your organization in AWS Organizations\. If you add a new account to the organization, Firewall Manager automatically applies the policy to that account\.

1. Choose the types of resources that you want to protect\.

1. If you want to protect only resources with specific tags, or alternatively exclude resources with specific tags, select **Use tags to include/exclude resources**, enter the tags, and then choose either **Include** or **Exclude**\. You can choose only one option\. 

   If you enter more than one tag \(separated by commas\), and if a resource has any of those tags, it is considered a match\.

   For more information about tags, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\.

1. Choose **Create and apply this policy to existing and new resources**\.

   This option creates a web ACL in each applicable account within an organization in AWS Organizations, and associates the web ACL with the specified resources in the accounts\. This option also applies the policy to all new resources that match the preceding criteria \(resource type and tags\)\. Alternatively, if you choose **Create but do not apply this policy to existing or new resources**, Firewall Manager creates a web ACL in each applicable account within the organization, but doesn't apply the web ACL to any resources\. You must apply the policy to resources later\.

1. Leave the choice for **Replace existing associated web ACLs** at the default setting\.

   When this option is selected, Firewall Manager removed all existing web ACL associations from in\-scope resources before it associates the new policy's web ACLs to them\. 

1. Choose **Next**\.

1. Review the new policy\. To make any changes, choose **Edit**\. When you are satisfied with the policy, choose **Create policy**\.