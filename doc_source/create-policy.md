# Creating an AWS Firewall Manager Policy<a name="create-policy"></a>

The steps for creating a policy vary between the different policy types\. Make sure to use the procedure for the type of policy that you need\.

**Important**  
AWS Firewall Manager doesn't support Amazon Route 53 or AWS Global Accelerator\. If you want to protect these resources with Shield Advanced, you can't use a Firewall Manager policy\. Instead, follow the instructions in [Adding AWS Shield Advanced Protection to More AWS Resources](configure-new-protection.md)\. 

**Topics**
+ [Creating an AWS Firewall Manager Policy for AWS WAF Classic](#creating-firewall-manager-policy-for-waf)
+ [Creating an AWS Firewall Manager Policy for Shield Advanced](#creating-firewall-manager-policy-for-shield-advanced)
+ [Creating an AWS Firewall Manager Common Security Group Policy](#creating-firewall-manager-policy-common-security-group)
+ [Creating an AWS Firewall Manager Content Audit Security Group Policy](#creating-firewall-manager-policy-audit-security-group)
+ [Creating an AWS Firewall Manager Usage Audit Security Group Policy](#creating-firewall-manager-policy-usage-security-group)

## Creating an AWS Firewall Manager Policy for AWS WAF Classic<a name="creating-firewall-manager-policy-for-waf"></a>

**Note**  
The latest version of AWS WAF was released in November, 2019\. AWS Firewall Manager currently works with the prior version, AWS WAF Classic, and not AWS WAF\. For information about AWS WAF Classic, see [AWS WAF Classic](classic-waf-chapter.md) <a name="create-policy-procedure"></a>

**To create a Firewall Manager policy for AWS WAF Classic \(console\)**

1. Sign in to the AWS Management Console using the Firewall Manager administrator account that you set up in the prerequisites \([AWS Firewall Manager Prerequisites](fms-prereq.md)\), and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [Step 2: Set the AWS Firewall Manager Administrator Account](enable-integration.md)\.

1. In the navigation pane, choose **Security policies**\.

1. Choose **Create policy**\.

1. If you already created the AWS WAF Classic rule group that you want to add to the policy, choose **Create an AWS Firewall Manager policy and add existing rule groups**\. If you want to create a new rule group, choose **Create a Firewall Manager policy and add a new rule group**\.

1. If you are using an existing rule group, skip this step and go to the next step\. If you are creating a rule group, follow the instructions in [Creating a Rule Group](create-rule-group.md)\. After you create the rule group, continue with the following steps\.

1. Enter a policy name\.

1. For **Policy type**, choose **WAF**\. 

1. For **Region**, choose an AWS Region\. To protect Amazon CloudFront resources, choose **Global**\.

   To protect resources in multiple Regions \(other than CloudFront resources\), you must create separate Firewall Manager policies for each Region\.

1. Select a rule group to add, and then choose **Add rule group**\. 

1. A policy has two possible actions: **Action set by rule group** and **Count**\. If you want to test the policy and rule group, set the action to **Count**\. This action overrides any *block* action specified by the rule group contained in the policy\. That is, if the policy's action is set to **Count**, those requests are only counted and not blocked\. Conversely, if you set the policy's action to **Action set by rule group**, actions of the rule group in the policy are used\. Choose the appropriate action\.

1. Choose **Next**\.

1. If you want to include only specific accounts in the policy, or alternatively exclude specific accounts from the policy, select **Select accounts to include/exclude from this policy \(optional\)**\. Choose either **Include only these accounts in this policy** or **Exclude these accounts from this policy**\. You can choose only one option\. Choose **Add**\. Select the account numbers to include or exclude, and then choose **OK**\. 
**Note**  
If you don't select this option, Firewall Manager applies a policy to all accounts in your AWS organization\. If you add a new account to the organization, Firewall Manager automatically applies the policy to that account\.

1. Choose the type of resource that you want to protect\.

1. If you want to protect only resources with specific tags, or alternatively exclude resources with specific tags, select **Use tags to include/exclude resources**, enter the tags, and then choose either **Include** or **Exclude**\. You can choose only one option\. 

   If you enter more than one tag \(separated by commas\), if a resource has any of those tags, it is considered a match\.

   For more information about tags, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\.

1. If you want to automatically apply the policy to existing resources, choose **Create and apply this policy to existing and new resources**\.

   This option creates a web ACL in each applicable account within an AWS organization and associates the web ACL with the resources in the accounts\. This option also applies the policy to all new resources that match the preceding criteria \(resource type and tags\)\. Alternatively, if you choose **Create policy but do not apply the policy to existing or new resources**, Firewall Manager creates a web ACL in each applicable account within the organization, but doesn't apply the web ACL to any resources\. You must apply the policy to resources later\. Choose the appropriate option\.

1. Choose **Next**\.

1. Review the new policy\. To make any changes, choose **Edit**\. When you are satisfied with the policy, choose **Create and apply policy**\.

## Creating an AWS Firewall Manager Policy for Shield Advanced<a name="creating-firewall-manager-policy-for-shield-advanced"></a><a name="get-started-fms-shield-create-security-policy-procedure"></a>

**To create a Firewall Manager policy for Shield Advanced \(console\)**

1. Sign in to the AWS Management Console using the Firewall Manager administrator account that you set up in the prerequisites \([AWS Firewall Manager Prerequisites](fms-prereq.md)\), and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [Step 2: Set the AWS Firewall Manager Administrator Account](enable-integration.md)\.

1. In the navigation pane, choose **Security policies**\.

1. Choose **Create policy**\.

1. For **Name**, enter a friendly name\. 

1. For **Policy type**, choose **Shield Advanced**\. 

   To create a Shield Advanced policy, you must be subscribed to Shield Advanced\. If you are not subscribed, you are prompted to do so\. For more information, see [AWS Shield Advanced Pricing](aws-shield-pricing.md)\. 

1. For **Region**, choose an AWS Region\. To protect Amazon CloudFront resources, choose **Global**\.

   To protect resources in multiple Regions \(other than CloudFront resources\), you must create separate Firewall Manager policies for each Region\.

1. Choose **Next**\.

1. If you want to include only specific accounts in the policy, or alternatively exclude specific accounts from the policy, select **Select accounts to include/exclude from this policy \(optional\)**\. Choose either **Include only these accounts in this policy** or **Exclude these accounts from this policy**\. You can choose only one option\. Choose **Add**\. Select the account numbers to include or exclude, and then choose **OK**\. 
**Note**  
If you don't select this option, Firewall Manager applies a policy to all accounts in your AWS organization\. If you add a new account to the organization, Firewall Manager automatically applies the policy to that account\.

1. Choose the type of resource that you want to protect\.

   Firewall Manager does not support Amazon Route 53 or AWS Global Accelerator\. If you need to protect these resources with Shield Advanced, you can't use a Firewall Manager policy\. Instead, follow the instructions in [Adding AWS Shield Advanced Protection to More AWS Resources](configure-new-protection.md)\.

1. If you want to protect only resources with specific tags, or alternatively exclude resources with specific tags, select **Use tags to include/exclude resources**, enter the tags, and then choose either **Include** or **Exclude**\. You can choose only one option\. 

   If you enter more than one tag \(separated by commas\), and if a resource has any of those tags, it is considered a match\.

   For more information about tags, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\.

1. Choose **Create and apply this policy to existing and new resources**\.

   This option applies Shield Advanced protection to each applicable account within an AWS organization, and associates the protection with the specified resources in the accounts\. This option also applies the policy to all new resources that match the preceding criteria \(resource type and tags\)\. Alternatively, if you choose **Create but do not apply this policy to existing or new resources**, Firewall Manager doesn't apply Shield Advanced protection to any resources\. You must apply the policy to resources later\.

1. Choose **Next**\.

1. Review the new policy\. To make any changes, choose **Edit**\. When you are satisfied with the policy, choose **Create policy**\.

## Creating an AWS Firewall Manager Common Security Group Policy<a name="creating-firewall-manager-policy-common-security-group"></a>

To create a common security group policy, you must have a security group already created in your Firewall Manager administrator account that you want to use as the primary for your policy\. You can manage security groups through Amazon Virtual Private Cloud \(Amazon VPC\) or Amazon Elastic Compute Cloud \(Amazon EC2\)\. For information, see [Working with Security Groups](https://docs.aws.amazon.com/vpc/latest/userguide//VPC_SecurityGroups.html#WorkingWithSecurityGroups) in the [Amazon VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/)\. 

For information about how common security group policies work, see [Common Security Group Policies](security-group-policies.md#security-group-policies-common)\.

**To create a common security group policy \(console\)**

1. Sign in to the AWS Management Console using the Firewall Manager administrator account that you set up in the prerequisites \([AWS Firewall Manager Prerequisites](fms-prereq.md)\), and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [Step 2: Set the AWS Firewall Manager Administrator Account](enable-integration.md)\.

1. In the navigation pane, choose **Security policies**\.

1. Choose **Create policy**\.

1. For **Policy type**, choose **Security group**\. 

1. For **Security group policy type**, choose **Common security groups**\.

1. For **Region**, choose an AWS Region\. 

1. Choose **Next**\.

1. For **Policy name**, enter a friendly name\. 

1. For **Policy rules**, do the following: 

   1. From the rules options, choose the restrictions that you want to apply to the security group rules and the resources that are within policy scope\. 

   1. For **Primary security groups**, choose **Add primary security group**, and then choose the security group that you want to use\. Firewall Manager populates the list of primary security groups from all Amazon VPC instances in the Firewall Manager administrator account\. The default maximum number of primary security groups for a policy is one\. For information on increasing the maximum, see [AWS Firewall Manager Quotas](fms-limits.md)\.

   1. For **Policy action**, we recommend creating the policy with the option that doesn't automatically remediate\. This allows you to assess the effects of your new policy before you apply it\. When you are satisfied that the changes are what you want, then edit the policy and change the policy action to enable automatic remediation of noncompliant resources\. 

1. Choose **Next**\.

1. For **AWS accounts affected by this policy**, if you want to apply the policy to all accounts in your organization, choose **Include all accounts under my organization**\. If you want to include only specific accounts in the policy, or alternatively exclude specific accounts from the policy, choose one of those options, and then use the **AWS accounts** dialog box to add account numbers to include or exclude\. You can choose only one option\. 
**Note**  
For the choices **Include all accounts under my organization** and **Exclude the specified accounts and include all others**, when you add a new account to your organization, Firewall Manager automatically applies the policy to that account\.

1. For **Resource type**, choose the types of resource that you want to protect\.

1. For **Resources**, if you want to apply the policy to all resources within the AWS accounts and resource type parameters, choose **Include all resources that match the selected resource type**\. If you want to include or exclude specific resources, use tagging to specify the resources, and then choose the appropriate option and add the tags to the list\. You can apply the policy either to all resources except those that have all the tags that you specify, or you can apply it to only those that have all the tags that you specify\. For more information about tagging your resources, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\. 
**Note**  
If you enter more than one tag, a resource must have all the tags to be a match\.

1. Choose **Next**\.

1. Review the policy settings to be sure they're what you want, and then choose **Create policy**\.

Firewall Manager creates a replica of the primary security group in every Amazon VPC instance contained within the in\-scope accounts up to the supported Amazon VPC maximum quota per account\. Firewall Manager associates the replica security groups to the resources that are within policy scope for each in\-scope account\. For more information about how this policy works, see [Common Security Group Policies](security-group-policies.md#security-group-policies-common)\.

## Creating an AWS Firewall Manager Content Audit Security Group Policy<a name="creating-firewall-manager-policy-audit-security-group"></a>

To create a content audit security group policy, you must have a security group already created in your Firewall Manager administrator account that you want to use as the audit security group for your policy\. You can manage security groups through Amazon Virtual Private Cloud \(Amazon VPC\) or Amazon Elastic Compute Cloud \(Amazon EC2\)\. For information, see [Working with Security Groups](https://docs.aws.amazon.com/vpc/latest/userguide//VPC_SecurityGroups.html#WorkingWithSecurityGroups) in the [Amazon VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/)\. 

You can use the audit security group rules as a template for what rules are allowed by the policy or a template for what rules are denied by the policy\. For information about how content audit security group policies work, see [Content Audit Security Group Policies](security-group-policies.md#security-group-policies-audit)\. 

**To create a content audit security group policy \(console\)**

1. Sign in to the AWS Management Console using the Firewall Manager administrator account that you set up in the prerequisites \([AWS Firewall Manager Prerequisites](fms-prereq.md)\), and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [Step 2: Set the AWS Firewall Manager Administrator Account](enable-integration.md)\.

1. In the navigation pane, choose **Security policies**\.

1. Choose **Create policy**\.

1. For **Policy type**, choose **Security group**\. 

1. For **Security group policy type**, choose **Auditing and enforcement of security group rules**\.

1. For **Region**, choose an AWS Region\. 

1. Choose **Next**\.

1. For **Policy name**, enter a friendly name\. 

1. For **Policy rules**, do the following: 

   1. From the rules options, choose whether to allow only the rules defined in the audit security groups or deny all the rules\. For information on this choice, see [Content Audit Security Group Policies](security-group-policies.md#security-group-policies-audit)\. 

   1. For **Audit security groups**, choose **Add audit security groups**, and then choose the security group that you want to use\. Firewall Manager populates the list of audit security groups from all Amazon VPC instances in the Firewall Manager administrator account\. The default maximum quota for the number of audit security groups for a policy is one\. For information on increasing the quota, see [AWS Firewall Manager Quotas](fms-limits.md)\.

   1. For **Policy action**, you must create the policy with the option that doesn't automatically remediate\. This allows you to assess the effects of your new policy before you apply it\. When you are satisfied that the changes are what you want, edit the policy and change the policy action to enable automatic remediation of noncompliant resources\. 

1. Choose **Next**\.

1. For **AWS accounts affected by this policy**, if you want to apply the policy to all accounts in your organization, choose **Include all accounts under my organization**\. If you want to include only specific accounts in the policy, or alternatively exclude specific accounts from the policy, choose one of those options, and then use the **AWS accounts** dialog box to add account numbers to include or exclude\. You can choose only one option\. 
**Note**  
For the choices **Include all accounts under my organization** and **Exclude the specified accounts and include all others**, when you add a new account to your organization, Firewall Manager automatically applies the policy to that account\.

1. For **Resource type**, choose the types of resource that you want to protect\.

1. For **Resources**, if you want to apply the policy to all resources within the AWS accounts and resource type parameters, choose **Include all resources that match the selected resource type**\. If you want to include or exclude specific resources, use tagging to specify the resources, and then choose the appropriate option and add the tags to the list\. You can apply the policy either to all resources except those that have all the tags that you specify, or you can apply it to only those that have all the tags that you specify\. For more information about tagging your resources, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\. 
**Note**  
If you enter more than one tag, a resource must have all the tags to be a match\.

1. Choose **Next**\.

1. Review the policy settings to be sure they're what you want, and then choose **Create policy**\.

Firewall Manager compares the audit security group against the in\-scope security groups in your AWS organization, according to your policy rules settings\. You can review the policy status in the AWS Firewall Manager policy console\. After the policy is created, you can edit it and enable automatic remediation to put your auditing security group policy into effect\. For more information about how this policy works, see [Content Audit Security Group Policies](security-group-policies.md#security-group-policies-audit)\.

## Creating an AWS Firewall Manager Usage Audit Security Group Policy<a name="creating-firewall-manager-policy-usage-security-group"></a>

AWS Firewall Manager usage audit security group policies allow you to monitor your organization for unused and redundant security groups and optionally perform cleanup\. For information about how usage audit security group policies work, see [Usage Audit Security Group Policies](security-group-policies.md#security-group-policies-usage)\.

**To create a usage audit security group policy \(console\)**

1. Sign in to the AWS Management Console using the Firewall Manager administrator account that you set up in the prerequisites \([AWS Firewall Manager Prerequisites](fms-prereq.md)\), and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [Step 2: Set the AWS Firewall Manager Administrator Account](enable-integration.md)\.

1. In the navigation pane, choose **Security policies**\.

1. Choose **Create policy**\.

1. For **Policy type**, choose **Security group**\. 

1. For **Security group policy type**, choose **Auditing and cleanup of unused and redundant security groups**\.

1. For **Region**, choose an AWS Region\. 

1. Choose **Next**\.

1. For **Policy name**, enter a friendly name\. 

1. For **Policy rules**, choose one or both of the options available\. 
   + If you choose **Security groups within this policy scope must be used by at least one resource\.**, Firewall Manager removes any unused security groups\. If you choose this, Firewall Manager runs it last when you save the policy\. 
   + If you choose **Security groups within this policy scope must be unique\.**, Firewall Manager consolidates redundant security groups, so that only one is associated with any resources\. If you choose this, Firewall Manager runs it first when you save the policy\. 

1. For **Policy action**, we recommend creating the policy with the option that doesn't automatically remediate\. This allows you to assess the effects of your new policy before you apply it\. When you are satisfied that the changes are what you want, then edit the policy and change the policy action to enable automatic remediation of noncompliant resources\. 

1. Choose **Next**\.

1. For **AWS accounts affected by this policy**, if you want to apply the policy to all accounts in your organization, choose **Include all accounts under my organization**\. If you want to include only specific accounts in the policy, or alternatively exclude specific accounts from the policy, choose one of those options, and then use the **AWS accounts** dialog box to add account numbers to include or exclude\. You can choose only one option\. 
**Note**  
For the choices **Include all accounts under my organization** and **Exclude the specified accounts and include all others**, when you add a new account to your organization, Firewall Manager automatically applies the policy to that account\.

1. For **Resources**, if you want to apply the policy to all resources within the AWS accounts and resource type parameters, choose **Include all resources that match the selected resource type**\. If you want to include or exclude specific resources, use tagging to specify the resources, and then choose the appropriate option and add the tags to the list\. You can apply the policy either to all resources except those that have all the tags that you specify, or you can apply it to only those that have all the tags that you specify\. For more information about tagging your resources, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\. 
**Note**  
If you enter more than one tag, a resource must have all the tags to be a match\.

1. Choose **Next**\.

1. If you haven't excluded the Firewall Manager administrator account from the policy scope, Firewall Manager prompts you to do this\. Doing this leaves the security groups in the Firewall Manager administrator account, which you use for common and audit security group policies, under your manual control\. Choose the option you want in this dialogue\.

1. Review the policy settings to be sure they're what you want, and then choose **Create policy**\.
+ If you choose **Security groups within this policy scope must be used by at least one resource\.**, Firewall Manager removes any unused security groups\. If you choose this, Firewall Manager runs it last when you save the policy\. 
+ If you choose **Security groups within this policy scope must be unique\.**, Firewall Manager consolidates redundant security groups\. If you choose this, Firewall Manager runs it first when you save the policy\. 

If you chose to require unique security groups, Firewall Manager scans for redundant security groups in each in\-scope Amazon VPC instance\. Then, if you chose to require that each security group be used by at least one resource, Firewall Manager scans for unused security groups\. You can review the policy status in the AWS Firewall Manager policy console\. For more information about how this policy works, see [Usage Audit Security Group Policies](security-group-policies.md#security-group-policies-usage)\.