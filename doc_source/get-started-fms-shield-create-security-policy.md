# Step 2: Create and apply a Shield Advanced policy<a name="get-started-fms-shield-create-security-policy"></a>

After completing the prerequisites, you create an AWS Firewall Manager Shield Advanced policy\. A Firewall Manager Shield Advanced policy contains the accounts and resources that you want to protect with Shield Advanced\.

**Important**  
Firewall Manager does not support Amazon Route 53 or AWS Global Accelerator\. If you need to protect these resources with Shield Advanced, you can't use a Firewall Manager policy\. Instead, follow the instructions in [Adding AWS Shield Advanced protection to AWS resources](ddos-manage-protected-resources.md#configure-new-protection)\. 

**To create a Firewall Manager Shield Advanced policy \(console\)**

1. Sign in to the AWS Management Console using your Firewall Manager administrator account, and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fmsv2](https://console.aws.amazon.com/wafv2/fmsv2)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [AWS Firewall Manager prerequisites](fms-prereq.md)\.

1. In the navigation pane, choose **Security policies**\.

1. Choose **Create policy**\.

1. For **Policy type**, choose **Shield Advanced**\. 

   To create a Shield Advanced policy, your Firewall Manager administrator account must be subscribed to Shield Advanced\. If you are not subscribed, you are prompted to do so\. For information about the cost for subscribing, see [AWS Shield Advanced Pricing](http://aws.amazon.com/shield/pricing/)\.
**Note**  
You don't need to manually subscribe each member account to Shield Advanced\. Firewall Manager does this for you when it creates the policy\.

1. For **Region**, choose an AWS Region\. To protect Amazon CloudFront resources, choose **Global**\.

   To protect resources in multiple Regions \(other than CloudFront resources\), you must create separate Firewall Manager policies for each Region\.

1. Choose **Next**\.

1. For **Name**, enter a descriptive name\. 

1. \(Global Region only\) For **Global** Region policies, you can choose whether you want to manage Shield Advanced automatic application layer DDoS mitigation\. For this tutorial, leave this choice at the default setting of **Ignore**\.

1. For **Policy action**, choose the option that doesn't automatically remediate\. 

1. Choose **Next**\.

1. **AWS accounts this policy applies to** allows you to narrow the scope of your policy by specifying accounts to include or exclude\. For this tutorial, choose **Include all accounts under my organization\.** 

1. Choose the types of resources that you want to protect\.

   Firewall Manager doesn't support Amazon Route 53 or AWS Global Accelerator\. If you need to protect these resources with Shield Advanced, you can't use a Firewall Manager policy\. Instead, follow the Shield Advanced guidance at [Adding AWS Shield Advanced protection to AWS resources](ddos-manage-protected-resources.md#configure-new-protection)\.

1. If you want to protect only resources with specific tags, or alternatively exclude resources with specific tags, select **Use tags to include/exclude resources**, enter the tags separated by commas, and then choose either **Include** or **Exclude**\. You can choose only one option\. 

   If you enter more than one tag, and if a resource has any of those tags, it is considered a match\.

   For more information about tags, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\.

1. Choose **Next**\. 

1. For **Policy tags**, add any identifying tags that you want for the Firewall Manager policy\. For more information about tags, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\.

1. Choose **Next**\.

1. Review the new policy\. To make any changes, choose **Previous**\. When you are satisfied with the policy, choose **Create policy**\.

Continue to [Step 3: \(Optional\) authorize the Shield Response Team \(SRT\)](get-started-fms-shield-authorize-srt.md)\.