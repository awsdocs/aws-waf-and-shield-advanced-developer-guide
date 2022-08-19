# Getting started with AWS Firewall Manager​ AWS Shield Advanced policies<a name="getting-started-fms-shield"></a>

You can use AWS Firewall Manager to enable AWS Shield Advanced protections across your organization\. 

**Important**  
Firewall Manager doesn't support Amazon Route 53 or AWS Global Accelerator\. If you need to protect these resources with Shield Advanced, you can't use a Firewall Manager policy\. Instead, follow the instructions in [Adding AWS Shield Advanced protection to AWS resources](ddos-manage-protected-resources.md#configure-new-protection)\.

To use Firewall Manager to enable Shield Advanced protection, perform the following steps in sequence\. 

**Topics**
+ [Step 1: Complete the prerequisites](complete-prereq-fms-shield.md)
+ [Step 2: Create and apply an AWS Firewall Manager Shield Advanced policy](get-started-fms-shield-create-security-policy.md)
+ [Step 3: \(Optional\) authorize the Shield Response Team \(SRT\)](get-started-fms-shield-authorize-srt.md)
+ [Step 4: Configure Amazon SNS notifications and Amazon CloudWatch alarms](get-started-fms-shield-cloudwatch.md)

When you've completed your Shield Advanced configuration, familiarize yourself with your options for viewing events at [Visibility into DDoS events](ddos-viewing-events.md)\.