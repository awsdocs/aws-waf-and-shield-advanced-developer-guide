# Step 3: Create and apply a Palo Alto Networks Cloud NGFW policy<a name="get-started-fms-cloud-ngfw-create-policy"></a>

After completing the prerequisites, you create an AWS Firewall Manager Palo Alto Networks Cloud NGFW policy\.

For more information about Firewall Manager policies for Palo Alto Networks Cloud NGFW, see [Palo Alto Networks Cloud NGFW policies](cloud-ngfw-policies.md)\.

**To create a Firewall Manager policy for Palo Alto Networks Cloud NGFW \(console\)**

1. Sign in to the AWS Management Console using your Firewall Manager administrator account, and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fmsv2](https://console.aws.amazon.com/wafv2/fmsv2)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [AWS Firewall Manager prerequisites](fms-prereq.md)\.

1. In the navigation pane, choose **Security policies**\.

1. Choose **Create policy**\.

1. For **Policy type**, choose **Palo Alto Networks Palo Alto Networks Cloud NGFW**\. If you haven't already subscribed to the Palo Alto Networks Cloud NGFW service in the AWS Marketplace, you'll need to do that first\. To subscribe in the AWS Marketplace, choose **View AWS Marketplace details**\.

1. For **Deployment model**, choose either the **Distributed model** or **Centralized model**\. The deployment model determines how Firewall Manager manages endpoints for the policy\. With the distributed model, Firewall Manager maintains firewall endpoints in each VPC that's within policy scope\. With the centralized model, Firewall Manager maintains a single endpoint in an inspection VPC\.

1. For **Region**, choose an AWS Region\. To protect resources in multiple Regions, you must create separate policies for each Region\. 

1. Choose **Next**\.

1. For **Policy name**, enter a descriptive name\.

1. In the policy configuration, choose the Palo Alto Networks Cloud NGFW firewall policy to associate with this policy\. The list of Palo Alto Networks Cloud NGFW firewall policies contains all of the Palo Alto Networks Cloud NGFW firewall policies that are associated with your Palo Alto Networks Cloud NGFW tenant\. For information about creating and managing Palo Alto Networks Cloud NGFW firewall policies, see the *[Deploy Palo Alto Networks Cloud NGFW for AWS with the AWS Firewall Manager](https://docs.paloaltonetworks.com/cloud-ngfw/aws/cloud-ngfw-on-aws/getting-started-with-cloud-ngfw-for-aws/deploy-cloud-ngfw-for-aws-with-the-aws-firewall-manager.html)* topic in the *Palo Alto Networks Palo Alto Networks Cloud NGFW for AWS deployment guide*\.

1. For **Palo Alto Networks Palo Alto Networks Cloud NGFW logging \- optional**, optionally choose which Palo Alto Networks Cloud NGFW log type\(s\) to log for your policy\. For information about Palo Alto Networks Cloud NGFW log types, see [Configure Logging for Palo Alto Networks Cloud NGFW on AWS](https://docs.paloaltonetworks.com/cloud-ngfw/aws/cloud-ngfw-on-aws/create-cloud-ngfw-instances-and-endpoints/configure-logging-for-the-cloud-ngfw-on-aws.html) in the *Palo Alto Networks Palo Alto Networks Cloud NGFW for AWS deployment guide*\.

   For **log destination**, specify when Firewall Manager should write logs to\.

1. Choose **Next**\.

1. Under **Configure third\-party firewall endpoint** do one of the following, depending on whether you're using the distributed or centralized deployment model to create your firewall endpoints:
   + If you're using the distributed deployment model for this policy, under **Availability Zones**, select which Availability Zones to create firewall endpoints in\. You can select Availability Zones by **Availability Zone name** or by **Availability Zone ID**\.
   + If you're using the centralized deployment model for this policy, in **AWS Firewall Manager endpoint configuration** under **Inspection VPC configuration**, enter the AWS account ID of the owner of the inspection VPC, and the VPC ID of the inspection VPC\.
     + Under **Availability Zones**, select which Availability Zones to create firewall endpoints in\. You can select Availability Zones by **Availability Zone name** or by **Availability Zone ID**\.

1. Choose **Next**\.

1. For **Policy scope**, under **AWS accounts this policy applies to**, choose the option as follows: 
   + If you want to apply the policy to all accounts in your organization, leave the default selection, **Include all accounts under my AWS organization**\. 
   + If you want to apply the policy only to specific accounts or accounts that are in specific AWS Organizations organizational units \(OUs\), choose **Include only the specified accounts and organizational units**, and then add the accounts and OUs that you want to include\. Specifying an OU is the equivalent of specifying all accounts in the OU and in any of its child OUs, including any child OUs and accounts that are added at a later time\. 
   + If you want to apply the policy to all but a specific set of accounts or AWS Organizations organizational units \(OUs\), choose **Exclude the specified accounts and organizational units, and include all others**, and then add the accounts and OUs that you want to exclude\. Specifying an OU is the equivalent of specifying all accounts in the OU and in any of its child OUs, including any child OUs and accounts that are added at a later time\. 

   You can only choose one of the options\. 

   After you apply the policy, Firewall Manager automatically evaluates any new accounts against your settings\. For example, if you include only specific accounts, Firewall Manager doesn't apply the policy to any new accounts\. As another example, if you include an OU, when you add an account to the OU or to any of its child OUs, Firewall Manager automatically applies the policy to the new account\.

1. The **Resource type** for Network Firewall policies is **VPC**\. 

1. For **Resources**, if you want to protect \(or exclude\) only resources that have specific tags, select the appropriate option, then enter the tags to include or exclude\. You can choose only one option\. For more information about tags, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\. 

   If you enter more than one tag, a resource must have all of the tags to be included or excluded\.

1. For **Grant cross\-account access**, choose **Download AWS CloudFormation template**\. This downloads a AWS CloudFormation template that you can use to create a AWS CloudFormation stack\. This stack creates an AWS Identity and Access Management role that grants Firewall Manager cross\-account permissions to manage Palo Alto Networks Cloud NGFW resources\. For information about stacks, see [Working with stacks](https://docs.aws.amazon.com/AWSCloudFormation/latest/gsg/stacks.html) in the *AWS CloudFormation User Guide*\.

1. Choose **Next**\.

1. For **Policy tags**, add any identifying tags that you want for the Firewall Manager policy\. For more information about tags, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\.

1. Choose **Next**\.

1. Review the new policy\. To make any changes, choose **Edit** in the area that you want to change\. This returns you to the corresponding step in the creation wizard\. When you are satisfied with the policy, choose **Create policy**\.

For more information about Firewall Manager Palo Alto Networks Cloud NGFW policies, see [Palo Alto Networks Cloud NGFW policies](cloud-ngfw-policies.md)\.