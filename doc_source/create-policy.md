# Creating an AWS Firewall Manager Policy<a name="create-policy"></a>

When you create an AWS Firewall Manager policy, you specify which rule group to add to the policy\.<a name="create-policy-procedure"></a>

**To create a Firewall Manager policy \(console\)**

1. Sign in to the AWS Management Console using the Firewall Manager administrator account that you set up in the prerequisites, and then open the Firewall Manager console at https://console\.aws\.amazon\.com/waf/fms\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [Step 2: Set the AWS Firewall Manager Administrator Account](enable-integration.md)\.

1. In the navigation pane, choose **Security policies**\.

1. Choose **Create policy**\.

1. If you already created the rule group that you want to add to the policy, choose **Create an AWS Firewall Manager policy and add existing rule groups**\. If you want to create a new rule group, choose **Create an AWS Firewall Manager policy and add a new rule group**\.

1. If you are using an existing rule group, skip this step and go to the next step\. If you are creating a rule group, follow the instructions in [Creating a Rule Group](create-rule-group.md)\. After you create the rule group, continue with the following steps\.

1. Type a policy name\.

1. For **Region**, choose an AWS Region\.

1. Select a rule group to add, and then choose **Add rule group**\. 

1. A policy has two possible actions: **Action set by rule group** and **Count**\. If you want to test the policy and rule group, set the action to **Count**\. This action overrides any *block* action specified by the rule group contained in the policy\. That is, if the policy's action is set to **Count**, those requests are only counted and not blocked\. Conversely, if you set the policy's action to **Action set by rule group**, actions of the rule group in the policy are used\. Choose the appropriate action\.

1. Choose **Next**\.

1. Choose the type of resource that you want to protect\.

   You can select only one type of resource per policy\.

1. If you want to protect only resources with specific tags, or alternatively exclude resources with specific tags, select **Use tags to include/exclude resources**, type the tags and then choose either **Include** or **Exclude**\. You can choose only one option\. 

   If you enter more than one tag \(separated by commas\), if a resource has any of those tags, it is considered a match\.

   For more information about tags, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html) \.

1. If you want to automatically apply the policy to existing resources, choose **Create and apply this policy to existing and new resources**\.

   This option creates a web ACL in each account within an organization in AWS Organizations and associates the web ACL with the resources in the accounts\. This option also applies the policy to all new resources that match the preceding criteria \(resource type and tags\)\. Alternatively, if you choose **Create policy but do not apply the policy to existing or new resources**, Firewall Manager creates a web ACL in each account within the organization, but doesn't apply the web ACL to any resources\. You must apply the policy to resources later\. Choose the appropriate option\.

1. Choose **Next**\.

1. Review the new policy\. To make any changes, choose **Edit**\. When you are satisfied with the policy, choose **Create and apply policy**\.
**Note**  
Firewall Manager applies a policy to all accounts in your organization in AWS Organizations\. You can't include or exclude individual accounts\. If you add a new account to the organization, Firewall Manager automatically applies the policy to that account\.