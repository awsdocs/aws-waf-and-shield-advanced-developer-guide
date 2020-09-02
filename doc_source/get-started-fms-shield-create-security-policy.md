# Step 2: Create and apply an AWS Firewall Manager Shield Advanced policy<a name="get-started-fms-shield-create-security-policy"></a>

After completing the prerequisites, you create an AWS Firewall Manager Shield Advanced policy\. A Firewall Manager Shield Advanced policy contains the accounts and resources that you want to protect with Shield Advanced\.

**Important**  
Firewall Manager does not support Amazon Route 53 or AWS Global Accelerator\. If you need to protect these resources with Shield Advanced, you can't use a Firewall Manager policy\. Instead, follow the instructions in [Adding AWS Shield Advanced protection to AWS resources](configure-new-protection.md)\. <a name="get-started-fms-shield-create-security-policy-procedure"></a>

**To create a Firewall Manager Shield Advanced policy \(console\)**

1. Sign in to the AWS Management Console using the Firewall Manager administrator account that you set up in the prerequisites, and then open the Firewall Manager console at [https://console\.aws\.amazon\.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [Step 2: Set the AWS Firewall Manager administrator account](enable-integration.md)\.

1. In the navigation pane, choose **Security policies**\.

1. Choose **Create policy**\.

1. For **Policy type**, choose **Shield Advanced**\. 

   To create a Shield Advanced policy, your Firewall Manager administrator account must be subscribed to Shield Advanced\. If you are not subscribed, you are prompted to do so\. For more information, see [AWS Shield pricing](aws-shield-pricing.md)\.
**Note**  
You don't need to manually subscribe each member account to Shield Advanced\. Firewall Manager does this for you as part of creating the policy\.

1. For **Region**, choose an AWS Region\. To protect Amazon CloudFront resources, choose **Global**\.

   To protect resources in multiple Regions \(other than CloudFront resources\), you must create separate Firewall Manager policies for each Region\.

1. Choose **Next**\.

1. For **Name**, enter a friendly name\. 

1. **AWS accounts affected by this policy** allows you to narrow the scope of your policy by specifying accounts to include or exclude\. For this tutorial, choose **Include all accounts under my organization\.** 

1. Choose the types of resources that you want to protect\.

   Firewall Manager doesn't support Amazon Route 53 or AWS Global Accelerator\. If you need to protect these resources with Shield Advanced, you can't use a Firewall Manager policy\. Instead, follow the instructions in [Adding AWS Shield Advanced protection to AWS resources](configure-new-protection.md)\.

1. If you want to protect only resources with specific tags, or alternatively exclude resources with specific tags, select **Use tags to include/exclude resources**, enter the tags, and then choose either **Include** or **Exclude**\. You can choose only one option\. 

   If you enter more than one tag \(separated by commas\), and if a resource has any of those tags, it is considered a match\.

   For more information about tags, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\.

1. Choose **Create and apply this policy to existing and new resources**\.

   This option applies Shield Advanced protection to each applicable account within an organization in AWS Organizations, and associates the protection with the specified resources in the accounts\. This option also applies the policy to all new resources that match the preceding criteria \(resource type and tags\)\. Alternatively, if you choose **Create but do not apply this policy to existing or new resources**, Firewall Manager doesn't apply Shield Advanced protection to any resources\. You must apply the policy to resources later\.
**Note**  
Shield Advanced protects up to 1,000 resources per account\.

1. Choose **Next**\.

1. Review the new policy\. To make any changes, choose **Previous**\. When you are satisfied with the policy, choose **Create policy**\.

Continue to [Step 3: \(Optional\) authorize the DDoS Response Team \(DRT\)](get-started-fms-shield-authorize-DRT.md)\.