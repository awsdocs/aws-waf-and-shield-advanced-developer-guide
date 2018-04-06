# Step 4: Create and Apply an AWS Firewall Manager Policy<a name="get-started-fms-create-security-policy"></a>

After you create the rule group, you create an AWS Firewall Manager policy\. A Firewall Manager policy contains the rule group that you want to apply to your resources\.<a name="get-started-fms-create-security-policy-procedure"></a>

**To create a Firewall Manager policy \(console\)**

1. After you create the rule group \(the last step in the preceding procedure, [Step 3: Create a Rule Group](get-started-fms-create-rule-group.md)\), the console displays the **Rule group summary** page\. Choose **Next**\.

1. For **Name**, type a friendly name\. 

1. For **Region**, choose an AWS Region\.

1. Select a rule group to add, and then choose **Add rule group**\. 

1. A policy has two possible actions: **Action set by rule group** and **Count**\. If you want to test the policy and rule group, set the action to **Count**\. This action overrides any *block* action specified by the rule group contained in the policy\. That is, if the policy's action is set to **Count**, those requests are only counted and not blocked\. Conversely, if you set the policy's action to **Action set by rule group**, actions of the rule group in the policy are used\. For this tutorial, choose **Count**\.

1. Choose **Next**\.

1. Choose the type of resource that you want to protect\.

1. If you want to protect only resources with specific tags, or alternatively exclude resources with specific tags, select **Use tags to include/exclude resources**, type the tags and then choose either **Include** or **Exclude**\. You can choose only one option\. 

   If you enter more than one tag \(separated by commas\), and if a resource has any of those tags, it is considered a match\.

   For more information about tags, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html) \.

1. Choose **Create and apply this policy to existing and new resources**\.

   This option creates a web ACL in each account within an organization in AWS Organizations, and associates the web ACL with the specified resources in the accounts\. This option also applies the policy to all new resources that match the above criteria \(resource type and tags\)\. Alternatively, if you choose **Create policy but do not apply the policy to existing or new resources**, Firewall Manager creates a web ACL in each account within the organization, but doesn't apply the web ACL to any resources\. You must apply the policy to resources later\.

1. Choose **Next**\.

1. Review the new policy\. To make any changes, choose **Edit**\. When you are satisfied with the policy, choose **Create policy**\.
**Note**  
Firewall Manager applies a policy to all accounts in your organization in AWS Organizations\. You can't include or exclude individual accounts\. If you add a new account to the organization, Firewall Manager automatically applies the policy to that account\.