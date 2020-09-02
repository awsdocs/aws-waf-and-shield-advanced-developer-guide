# Creating an AWS Firewall Manager policy<a name="create-policy"></a>

The steps for creating a policy vary between the different policy types\. Make sure to use the procedure for the type of policy that you need\.

**Important**  
AWS Firewall Manager doesn't support Amazon Route 53 or AWS Global Accelerator\. If you want to protect these resources with Shield Advanced, you can't use a Firewall Manager policy\. Instead, follow the instructions in [Adding AWS Shield Advanced protection to AWS resources](configure-new-protection.md)\. 

**Topics**
+ [Creating an AWS Firewall Manager policy for AWS WAF](#creating-firewall-manager-policy-for-waf)
+ [Creating an AWS Firewall Manager policy for AWS WAF Classic](#creating-firewall-manager-policy-for-classic-waf)
+ [Creating an AWS Firewall Manager policy for shield advanced](#creating-firewall-manager-policy-for-shield-advanced)
+ [Creating an AWS Firewall Manager common security group policy](#creating-firewall-manager-policy-common-security-group)
+ [Creating an AWS Firewall Manager content audit security group policy](#creating-firewall-manager-policy-audit-security-group)
+ [Creating an AWS Firewall Manager usage audit security group policy](#creating-firewall-manager-policy-usage-security-group)

## Creating an AWS Firewall Manager policy for AWS WAF<a name="creating-firewall-manager-policy-for-waf"></a>

In a Firewall Manager AWS WAF policy, you can use managed rule groups, which AWS and AWS Marketplace sellers create and maintain for you\. You can also create and use your own rule groups\. For more information about rule groups, see [Rule groups](waf-rule-groups.md)\.

If you want to use your own rule groups, create those before you create your Firewall Manager AWS WAF policy\. For guidance, see [Managing your own rule groups](waf-user-created-rule-groups.md)\. To use an individual custom rule, you must define your own rule group, define your rule within that, and then use the rule group in your policy\.

For information about Firewall Manager AWS WAF policies, see [AWS WAF policies](waf-policies.md)\.

**To create a Firewall Manager policy for AWS WAF \(console\)**

1. Sign in to the AWS Management Console using the Firewall Manager administrator account that you set up in the prerequisites \([AWS Firewall Manager prerequisites](fms-prereq.md)\), and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [Step 2: Set the AWS Firewall Manager administrator account](enable-integration.md)\.

1. In the navigation pane, choose **Security policies**\.

1. Choose **Create policy**\.

1. For **Policy type**, choose **AWS WAF**\. 

1. For **Region**, choose an AWS Region\. To protect Amazon CloudFront distributions, choose **Global**\.

   To protect resources in multiple Regions \(other than CloudFront distributions\), you must create separate Firewall Manager policies for each Region\.

1. Choose **Next**\.

1. For **Policy name**, enter a descriptive name\. Firewall Manager includes the policy name in the names of the web ACLs that it creates\. The web ACL names begin with `FMManagedWebACLV2` followed by the policy name that you enter here\. 

1. Under **Policy rules**, add the rule groups that you want AWS WAF to evaluate first and last in the web ACL\. The individual account managers can add rules and rule groups in between your first rule groups and your last rule groups\. For more information, see [AWS WAF policies](waf-policies.md)\.

1. Set the default action for the web ACL\. This is the action that AWS WAF takes when a web request doesn't match any of the rules in the web ACL\. For more information, see [Deciding on the default action for a Web ACL](web-acl-processing.md#web-acl-default-action)\.

1. For **Policy action**, if you want to create a web ACL in each applicable account within the organization, but not apply the web ACL to any resources yet, choose **Identify resources that don't comply with the policy rules, but don't auto remediate**\. You can change the option later\. 

   If instead you want to automatically apply the policy to existing in\-scope resources, choose **Auto remediate any noncompliant resources**\. This option creates a web ACL in each applicable account within the AWS organization and associates the web ACL with the resources in the accounts\.

   When you choose **Auto remediate any noncompliant resources**, you can also choose to remove existing web ACL associations from in\-scope resources, for the web ACLs that aren't managed by another active Firewall Manager policy\. If you choose this option, Firewall Manager first associates the policy's web ACL with the resources, and then removes the prior associations\. If a resource has an association with another web ACL that's managed by a different active Firewall Manager policy, this choice doesn't affect that association\. 

1. Choose **Next**\.

1. For **AWS accounts this policy applies to**, choose the option as follows: 
   + If you want to apply the policy to all accounts in your organization, leave the default selection, **Include all accounts under my AWS organization**\. 
   + If you want to apply the policy only to specific accounts or accounts that are in specific AWS Organizations organizational units \(OUs\), choose **Include only the specified accounts and organizational units**, and then add the accounts and OUs that you want to include\. Specifying an OU is the equivalent of specifying all accounts in the OU and in any of its child OUs, including any child OUs and accounts that are added at a later time\. 
   + If you want to apply the policy to all but a specific set of accounts or AWS Organizations organizational units \(OUs\), choose **Exclude the specified accounts and organizational units, and include all others**, and then add the accounts and OUs that you want to exclude\. Specifying an OU is the equivalent of specifying all accounts in the OU and in any of its child OUs, including any child OUs and accounts that are added at a later time\. 

   You can only choose one of the options\. 

   After you apply the policy, Firewall Manager automatically evaluates any new accounts against your settings\. For example, if you include only specific accounts, Firewall Manager doesn't apply the policy to any new accounts\. As another example, if you include an OU, when you add an account to the OU or to any of its child OUs, Firewall Manager automatically applies the policy to the new account\.

1. For **Resource type**, choose the types of resources that you want to protect\.

1. For **Resources**, if you want to protect \(or exclude\) only resources that have specific tags, select the appropriate option, then enter the tags to include or exclude\. You can choose only one option\. For more information about tags, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\. 

   If you enter more than one tag, a resource must have all of the tags to be included or excluded\.

1. Choose **Next**\.

1. For **Policy tags**, add any identifying tags that you want for the Firewall Manager AWS WAF policy\. For more information about tags, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\.

1. Choose **Next**\.

1. Review the new policy\. To make any changes, choose **Edit** in the area that you want to change\. This returns you to the corresponding step in the creation wizard\. When you are satisfied with the policy, choose **Create policy**\.

## Creating an AWS Firewall Manager policy for AWS WAF Classic<a name="creating-firewall-manager-policy-for-classic-waf"></a>

**To create a Firewall Manager policy for AWS WAF Classic \(console\)**

1. Sign in to the AWS Management Console using the Firewall Manager administrator account that you set up in the prerequisites \([AWS Firewall Manager prerequisites](fms-prereq.md)\), and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [Step 2: Set the AWS Firewall Manager administrator account](enable-integration.md)\.

1. In the navigation pane, choose **Security policies**\.

1. Choose **Create policy**\.

1. For **Policy type**, choose **AWS WAF Classic**\. 

1. If you already created the AWS WAF Classic rule group that you want to add to the policy, choose **Create an AWS Firewall Manager policy and add existing rule groups**\. If you want to create a new rule group, choose **Create a Firewall Manager policy and add a new rule group**\.

1. For **Region**, choose an AWS Region\. To protect Amazon CloudFront resources, choose **Global**\.

   To protect resources in multiple Regions \(other than CloudFront resources\), you must create separate Firewall Manager policies for each Region\.

1. Choose **Next**\.

1. If you are creating a rule group, follow the instructions in [Creating an AWS WAF Classic rule group](classic-create-rule-group.md)\. After you create the rule group, continue with the following steps\.

1. Enter a policy name\.

1. If you are adding an existing rule group, use the dropdown menu to select a rule group to add, and then choose **Add rule group**\. 

1. A policy has two possible actions: **Action set by rule group** and **Count**\. If you want to test the policy and rule group, set the action to **Count**\. This action overrides any *block* action specified by the rules in the rule group\. That is, if the policy's action is set to **Count**, those requests are only counted and not blocked\. Conversely, if you set the policy's action to **Action set by rule group**, actions of the rule group rules are used\. Choose the appropriate action\.

1. Choose **Next**\.

1. For **AWS accounts this policy applies to**, choose the option as follows: 
   + If you want to apply the policy to all accounts in your organization, leave the default selection, **Include all accounts under my AWS organization**\. 
   + If you want to apply the policy only to specific accounts or accounts that are in specific AWS Organizations organizational units \(OUs\), choose **Include only the specified accounts and organizational units**, and then add the accounts and OUs that you want to include\. Specifying an OU is the equivalent of specifying all accounts in the OU and in any of its child OUs, including any child OUs and accounts that are added at a later time\. 
   + If you want to apply the policy to all but a specific set of accounts or AWS Organizations organizational units \(OUs\), choose **Exclude the specified accounts and organizational units, and include all others**, and then add the accounts and OUs that you want to exclude\. Specifying an OU is the equivalent of specifying all accounts in the OU and in any of its child OUs, including any child OUs and accounts that are added at a later time\. 

   You can only choose one of the options\. 

   After you apply the policy, Firewall Manager automatically evaluates any new accounts against your settings\. For example, if you include only specific accounts, Firewall Manager doesn't apply the policy to any new accounts\. As another example, if you include an OU, when you add an account to the OU or to any of its child OUs, Firewall Manager automatically applies the policy to the new account\.

1. Choose the type of resource that you want to protect\.

1. If you want to protect only resources with specific tags, or alternatively exclude resources with specific tags, select **Use tags to include/exclude resources**, enter the tags, and then choose either **Include** or **Exclude**\. You can choose only one option\. 

   If you enter more than one tag \(separated by commas\), if a resource has any of those tags, it is considered a match\.

   For more information about tags, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\.

1. If you want to automatically apply the policy to existing resources, choose **Create and apply this policy to existing and new resources**\.

   This option creates a web ACL in each applicable account within an AWS organization and associates the web ACL with the resources in the accounts\. This option also applies the policy to all new resources that match the preceding criteria \(resource type and tags\)\. Alternatively, if you choose **Create policy but do not apply the policy to existing or new resources**, Firewall Manager creates a web ACL in each applicable account within the organization, but doesn't apply the web ACL to any resources\. You must apply the policy to resources later\. Choose the appropriate option\.

1. For **Replace existing associated web ACLs**, you can choose to remove any web ACL associations that are currently defined for in\-scope resources, and then replace them with associations to the web ACLs that you are creating with this policy\. By default, Firewall Manager doesn't remove existing web ACL associations before it adds the new ones\. If you want to remove the existing ones, choose this option\. 

1. Choose **Next**\.

1. Review the new policy\. To make any changes, choose **Edit**\. When you are satisfied with the policy, choose **Create and apply policy**\.

## Creating an AWS Firewall Manager policy for shield advanced<a name="creating-firewall-manager-policy-for-shield-advanced"></a><a name="get-started-fms-shield-create-security-policy-procedure"></a>

**To create a Firewall Manager policy for Shield Advanced \(console\)**

1. Sign in to the AWS Management Console using the Firewall Manager administrator account that you set up in the prerequisites \([AWS Firewall Manager prerequisites](fms-prereq.md)\), and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [Step 2: Set the AWS Firewall Manager administrator account](enable-integration.md)\.

1. In the navigation pane, choose **Security policies**\.

1. Choose **Create policy**\.

1. For **Name**, enter a meaningful name\. 

1. For **Policy type**, choose **Shield Advanced**\. 

   To create a Shield Advanced policy, you must be subscribed to Shield Advanced\. If you are not subscribed, you are prompted to do so\. For more information, see [AWS Shield pricing](aws-shield-pricing.md)\. 

1. For **Region**, choose an AWS Region\. To protect Amazon CloudFront resources, choose **Global**\.

   To protect resources in multiple Regions \(other than CloudFront resources\), you must create separate Firewall Manager policies for each Region\.

1. Choose **Next**\.

1. For **AWS accounts this policy applies to**, choose the option as follows: 
   + If you want to apply the policy to all accounts in your organization, leave the default selection, **Include all accounts under my AWS organization**\. 
   + If you want to apply the policy only to specific accounts or accounts that are in specific AWS Organizations organizational units \(OUs\), choose **Include only the specified accounts and organizational units**, and then add the accounts and OUs that you want to include\. Specifying an OU is the equivalent of specifying all accounts in the OU and in any of its child OUs, including any child OUs and accounts that are added at a later time\. 
   + If you want to apply the policy to all but a specific set of accounts or AWS Organizations organizational units \(OUs\), choose **Exclude the specified accounts and organizational units, and include all others**, and then add the accounts and OUs that you want to exclude\. Specifying an OU is the equivalent of specifying all accounts in the OU and in any of its child OUs, including any child OUs and accounts that are added at a later time\. 

   You can only choose one of the options\. 

   After you apply the policy, Firewall Manager automatically evaluates any new accounts against your settings\. For example, if you include only specific accounts, Firewall Manager doesn't apply the policy to any new accounts\. As another example, if you include an OU, when you add an account to the OU or to any of its child OUs, Firewall Manager automatically applies the policy to the new account\.

1. Choose the type of resource that you want to protect\.

   Firewall Manager does not support Amazon Route 53 or AWS Global Accelerator\. If you need to protect these resources with Shield Advanced, you can't use a Firewall Manager policy\. Instead, follow the instructions in [Adding AWS Shield Advanced protection to AWS resources](configure-new-protection.md)\.

1. If you want to protect only resources with specific tags, or alternatively exclude resources with specific tags, select **Use tags to include/exclude resources**, enter the tags, and then choose either **Include** or **Exclude**\. You can choose only one option\. 

   If you enter more than one tag \(separated by commas\), and if a resource has any of those tags, it is considered a match\.

   For more information about tags, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\.

1. Choose **Create and apply this policy to existing and new resources**\.

   This option applies Shield Advanced protection to each applicable account within an AWS organization, and associates the protection with the specified resources in the accounts\. This option also applies the policy to all new resources that match the preceding criteria \(resource type and tags\)\. Alternatively, if you choose **Create but do not apply this policy to existing or new resources**, Firewall Manager doesn't apply Shield Advanced protection to any resources\. You must apply the policy to resources later\.

1. Choose **Next**\.

1. Review the new policy\. To make any changes, choose **Edit**\. When you are satisfied with the policy, choose **Create policy**\.

## Creating an AWS Firewall Manager common security group policy<a name="creating-firewall-manager-policy-common-security-group"></a>

For information about how common security group policies work, see [Common security group policies](security-group-policies.md#security-group-policies-common)\.

To create a common security group policy, you must have a security group already created in your Firewall Manager administrator account that you want to use as the primary for your policy\. You can manage security groups through Amazon Virtual Private Cloud \(Amazon VPC\) or Amazon Elastic Compute Cloud \(Amazon EC2\)\. For information, see [Working with Security Groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#WorkingWithSecurityGroups) in the [Amazon VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/)\. 

**To create a common security group policy \(console\)**

1. Sign in to the AWS Management Console using the Firewall Manager administrator account that you set up in the prerequisites \([AWS Firewall Manager prerequisites](fms-prereq.md)\), and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [Step 2: Set the AWS Firewall Manager administrator account](enable-integration.md)\.

1. In the navigation pane, choose **Security policies**\.

1. Choose **Create policy**\.

1. For **Policy type**, choose **Security group**\. 

1. For **Security group policy type**, choose **Common security groups**\.

1. For **Region**, choose an AWS Region\. 

1. Choose **Next**\.

1. For **Policy name**, enter a friendly name\. 

1. For **Policy rules**, do the following: 

   1. From the rules options, choose the restrictions that you want to apply to the security group rules and the resources that are within policy scope\. 

   1. For **Primary security groups**, choose **Add primary security group**, and then choose the security group that you want to use\. Firewall Manager populates the list of primary security groups from all Amazon VPC instances in the Firewall Manager administrator account\. The default maximum number of primary security groups for a policy is one\. For information about increasing the maximum, see [AWS Firewall Manager quotas](fms-limits.md)\.

   1. For **Policy action**, we recommend creating the policy with the option that doesn't automatically remediate\. This allows you to assess the effects of your new policy before you apply it\. When you are satisfied that the changes are what you want, then edit the policy and change the policy action to enable automatic remediation of noncompliant resources\. 

1. Choose **Next**\.

1. For **AWS accounts this policy applies to**, choose the option as follows: 
   + If you want to apply the policy to all accounts in your organization, leave the default selection, **Include all accounts under my AWS organization**\. 
   + If you want to apply the policy only to specific accounts or accounts that are in specific AWS Organizations organizational units \(OUs\), choose **Include only the specified accounts and organizational units**, and then add the accounts and OUs that you want to include\. Specifying an OU is the equivalent of specifying all accounts in the OU and in any of its child OUs, including any child OUs and accounts that are added at a later time\. 
   + If you want to apply the policy to all but a specific set of accounts or AWS Organizations organizational units \(OUs\), choose **Exclude the specified accounts and organizational units, and include all others**, and then add the accounts and OUs that you want to exclude\. Specifying an OU is the equivalent of specifying all accounts in the OU and in any of its child OUs, including any child OUs and accounts that are added at a later time\. 

   You can only choose one of the options\. 

   After you apply the policy, Firewall Manager automatically evaluates any new accounts against your settings\. For example, if you include only specific accounts, Firewall Manager doesn't apply the policy to any new accounts\. As another example, if you include an OU, when you add an account to the OU or to any of its child OUs, Firewall Manager automatically applies the policy to the new account\.

1. For **Resource type**, choose the types of resources that you want to protect\. 

   If you choose **EC2 instance**, you can choose to include all elastic network interfaces in each Amazon EC2 instance or just the default interface in each instance\. If you have more than one elastic network interface in any in\-scope Amazon EC2 instance, choosing the option to include all interfaces allows Firewall Manager to apply the policy to all of them\. When you enable automatic remediation, if Firewall Manager can't apply the policy to all elastic network interfaces in an Amazon EC2 instance, it marks the instance as noncompliant\.

1. For **Resources**, if you want to apply the policy to all resources within the AWS accounts and resource type parameters, choose **Include all resources that match the selected resource type**\. If you want to include or exclude specific resources, use tagging to specify the resources, and then choose the appropriate option and add the tags to the list\. You can apply the policy either to all resources except those that have all the tags that you specify, or you can apply it to only those that have all the tags that you specify\. For more information about tagging your resources, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\. 
**Note**  
If you enter more than one tag, a resource must have all the tags to be a match\.

1. For **Shared VPC resources**, if you want to apply the policy to resources in shared VPCs, in addition to the VPCs that the accounts own, select **Include resources from shared VPCs**\. 

1. Choose **Next**\.

1. Review the policy settings to be sure they're what you want, and then choose **Create policy**\.

Firewall Manager creates a replica of the primary security group in every Amazon VPC instance contained within the in\-scope accounts up to the supported Amazon VPC maximum quota per account\. Firewall Manager associates the replica security groups to the resources that are within policy scope for each in\-scope account\. For more information about how this policy works, see [Common security group policies](security-group-policies.md#security-group-policies-common)\.

## Creating an AWS Firewall Manager content audit security group policy<a name="creating-firewall-manager-policy-audit-security-group"></a>

For information about how content audit security group policies work, see [Content audit security group policies](security-group-policies.md#security-group-policies-audit)\. 

For some content audit policy settings, you must provide an audit security group for Firewall Manager to use as a template\. For example, you might have an audit security group that contains all of the rules that you don't allow in any security group\. You must create these audit security groups using your Firewall Manager administrator account, before you can use them in your policy\. You can manage security groups through Amazon Virtual Private Cloud \(Amazon VPC\) or Amazon Elastic Compute Cloud \(Amazon EC2\)\. For information, see [Working with Security Groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#WorkingWithSecurityGroups) in the [Amazon VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/)\. 

**To create a content audit security group policy \(console\)**

1. Sign in to the AWS Management Console using the Firewall Manager administrator account that you set up in the prerequisites \([AWS Firewall Manager prerequisites](fms-prereq.md)\), and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [Step 2: Set the AWS Firewall Manager administrator account](enable-integration.md)\.

1. In the navigation pane, choose **Security policies**\.

1. Choose **Create policy**\.

1. For **Policy type**, choose **Security group**\. 

1. For **Security group policy type**, choose **Auditing and enforcement of security group rules**\.

1. For **Region**, choose an AWS Region\. 

1. Choose **Next**\.

1. For **Policy name**, enter a friendly name\. 

1. For **Policy rules**, choose the managed or custom policy rules option that you want to use\. 

   1. For **Configure managed audit policy rules**, do the following: 

      1. For **Configure security group rules to audit**, select the type of security group rules that you want your audit policy to apply to\. 

      1. If you want to do things like restrict the protocols, ports, and CIDR range settings that you allow in your security groups, choose **Audit overly permissive security group rules** and select the options that you want\. 

         For selections that use protocol lists, you can use existing lists and you can create new lists\. For information about protocol lists and how to use them in your policy, see [Managed lists](working-with-managed-lists.md) and [Using managed lists](working-with-managed-lists.md#using-managed-lists)\.

      1. If you want to enforce restrictions on what specific applications can do, choose **Audit high risk applications** and select the options that you want\. 

         The following selections are mutually exclusive: **Applications that can access local CIDR ranges only** and **Applications that can use public CIDR ranges**\. You can select at most one of them in any policy\.

         For selections that use application lists, you can use existing lists and you can create new lists\. For information about application lists and how to use them in your policy, see [Managed lists](working-with-managed-lists.md) and [Using managed lists](working-with-managed-lists.md#using-managed-lists)\.

      1. Use the **Overrides** settings to explicitly override other settings in the policy\. You can choose to always allow or always deny specific security group rules, regardless of whether they comply with the other options that you've set for the policy\. 

         For this option, you provide an audit security group as your allowed rules or denied rules template\. For **Audit security groups**, choose **Add audit security groups**, and then choose the security group that you want to use\. Firewall Manager populates the list of audit security groups from all Amazon VPC instances in the Firewall Manager administrator account\. The default maximum quota for the number of audit security groups for a policy is one\. For information about increasing the quota, see [AWS Firewall Manager quotas](fms-limits.md)\.

   1. For **Configure custom policy rules**, do the following: 

      1. From the rules options, choose whether to allow only the rules defined in the audit security groups or deny all the rules\. For information about this choice, see [Content audit security group policies](security-group-policies.md#security-group-policies-audit)\. 

      1. For **Audit security groups**, choose **Add audit security groups**, and then choose the security group that you want to use\. Firewall Manager populates the list of audit security groups from all Amazon VPC instances in the Firewall Manager administrator account\. The default maximum quota for the number of audit security groups for a policy is one\. For information about increasing the quota, see [AWS Firewall Manager quotas](fms-limits.md)\.

      1. For **Policy action**, you must create the policy with the option that doesn't automatically remediate\. This allows you to assess the effects of your new policy before you apply it\. When you are satisfied that the changes are what you want, edit the policy and change the policy action to enable automatic remediation of noncompliant resources\. 

1. Choose **Next**\.

1. For **AWS accounts this policy applies to**, choose the option as follows: 
   + If you want to apply the policy to all accounts in your organization, leave the default selection, **Include all accounts under my AWS organization**\. 
   + If you want to apply the policy only to specific accounts or accounts that are in specific AWS Organizations organizational units \(OUs\), choose **Include only the specified accounts and organizational units**, and then add the accounts and OUs that you want to include\. Specifying an OU is the equivalent of specifying all accounts in the OU and in any of its child OUs, including any child OUs and accounts that are added at a later time\. 
   + If you want to apply the policy to all but a specific set of accounts or AWS Organizations organizational units \(OUs\), choose **Exclude the specified accounts and organizational units, and include all others**, and then add the accounts and OUs that you want to exclude\. Specifying an OU is the equivalent of specifying all accounts in the OU and in any of its child OUs, including any child OUs and accounts that are added at a later time\. 

   You can only choose one of the options\. 

   After you apply the policy, Firewall Manager automatically evaluates any new accounts against your settings\. For example, if you include only specific accounts, Firewall Manager doesn't apply the policy to any new accounts\. As another example, if you include an OU, when you add an account to the OU or to any of its child OUs, Firewall Manager automatically applies the policy to the new account\.

1. For **Resource type**, choose the types of resource that you want to protect\.

1. For **Resources**, if you want to apply the policy to all resources within the AWS accounts and resource type parameters, choose **Include all resources that match the selected resource type**\. If you want to include or exclude specific resources, use tagging to specify the resources, and then choose the appropriate option and add the tags to the list\. You can apply the policy either to all resources except those that have all the tags that you specify, or you can apply it to only those that have all the tags that you specify\. For more information about tagging your resources, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\. 
**Note**  
If you enter more than one tag, a resource must have all the tags to be a match\.

1. Choose **Next**\.

1. Review the policy settings to be sure they're what you want, and then choose **Create policy**\.

Firewall Manager compares the audit security group against the in\-scope security groups in your AWS organization, according to your policy rules settings\. You can review the policy status in the AWS Firewall Manager policy console\. After the policy is created, you can edit it and enable automatic remediation to put your auditing security group policy into effect\. For more information about how this policy works, see [Content audit security group policies](security-group-policies.md#security-group-policies-audit)\.

## Creating an AWS Firewall Manager usage audit security group policy<a name="creating-firewall-manager-policy-usage-security-group"></a>

For information about how usage audit security group policies work, see [Usage audit security group policies](security-group-policies.md#security-group-policies-usage)\.

**To create a usage audit security group policy \(console\)**

1. Sign in to the AWS Management Console using the Firewall Manager administrator account that you set up in the prerequisites \([AWS Firewall Manager prerequisites](fms-prereq.md)\), and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [Step 2: Set the AWS Firewall Manager administrator account](enable-integration.md)\.

1. In the navigation pane, choose **Security policies**\.

1. Choose **Create policy**\.

1. For **Policy type**, choose **Security group**\. 

1. For **Security group policy type**, choose **Auditing and cleanup of unused and redundant security groups**\.

1. For **Region**, choose an AWS Region\. 

1. Choose **Next**\.

1. For **Policy name**, enter a friendly name\. 

1. For **Policy rules**, choose one or both of the options available\. 
   + If you choose **Security groups within this policy scope must be used by at least one resource\.**, Firewall Manager removes any security groups that it determines are unused\. By default, Firewall Manager considers security groups as noncompliant with this policy rule if they are unused for any length of time\. You can optionally specify a number of minutes that a security group can exist unused before it is considered noncompliant\. If you choose this rule, Firewall Manager runs it last when you save the policy\. 
   + If you choose **Security groups within this policy scope must be unique\.**, Firewall Manager consolidates redundant security groups, so that only one is associated with any resources\. If you choose this, Firewall Manager runs it first when you save the policy\. 

1. For **Policy action**, we recommend creating the policy with the option that doesn't automatically remediate\. This allows you to assess the effects of your new policy before you apply it\. When you are satisfied that the changes are what you want, then edit the policy and change the policy action to enable automatic remediation of noncompliant resources\. 

1. Choose **Next**\.

1. For **AWS accounts this policy applies to**, choose the option as follows: 
   + If you want to apply the policy to all accounts in your organization, leave the default selection, **Include all accounts under my AWS organization**\. 
   + If you want to apply the policy only to specific accounts or accounts that are in specific AWS Organizations organizational units \(OUs\), choose **Include only the specified accounts and organizational units**, and then add the accounts and OUs that you want to include\. Specifying an OU is the equivalent of specifying all accounts in the OU and in any of its child OUs, including any child OUs and accounts that are added at a later time\. 
   + If you want to apply the policy to all but a specific set of accounts or AWS Organizations organizational units \(OUs\), choose **Exclude the specified accounts and organizational units, and include all others**, and then add the accounts and OUs that you want to exclude\. Specifying an OU is the equivalent of specifying all accounts in the OU and in any of its child OUs, including any child OUs and accounts that are added at a later time\. 

   You can only choose one of the options\. 

   After you apply the policy, Firewall Manager automatically evaluates any new accounts against your settings\. For example, if you include only specific accounts, Firewall Manager doesn't apply the policy to any new accounts\. As another example, if you include an OU, when you add an account to the OU or to any of its child OUs, Firewall Manager automatically applies the policy to the new account\.

1. For **Resources**, if you want to apply the policy to all resources within the AWS accounts and resource type parameters, choose **Include all resources that match the selected resource type**\. If you want to include or exclude specific resources, use tagging to specify the resources, and then choose the appropriate option and add the tags to the list\. You can apply the policy either to all resources except those that have all the tags that you specify, or you can apply it to only those that have all the tags that you specify\. For more information about tagging your resources, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\. 
**Note**  
If you enter more than one tag, a resource must have all the tags to be a match\.

1. Choose **Next**\.

1. If you haven't excluded the Firewall Manager administrator account from the policy scope, Firewall Manager prompts you to do this\. Doing this leaves the security groups in the Firewall Manager administrator account, which you use for common and audit security group policies, under your manual control\. Choose the option you want in this dialogue\.

1. Review the policy settings to be sure they're what you want, and then choose **Create policy**\.

If you chose to require unique security groups, Firewall Manager scans for redundant security groups in each in\-scope Amazon VPC instance\. Then, if you chose to require that each security group be used by at least one resource, Firewall Manager scans for security groups that have remained unused for the minutes specified in the rule\. You can review the policy status in the AWS Firewall Manager policy console\. For more information about how this policy works, see [Usage audit security group policies](security-group-policies.md#security-group-policies-usage)\.