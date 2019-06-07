# Getting Started with AWS Firewall Manager to Enable AWS Shield Advanced Protection<a name="getting-started-fms-shield"></a>

You can use AWS Firewall Manager to enable both AWS WAF rules and AWS Shield Advanced protection\. However, the steps for AWS WAF and Shield Advanced are slightly different\. This topic shows you how to get started with Firewall Manager to enable Shield Advanced protection\. If you want to use Firewall Manager to enable AWS WAF rules, follow the steps in [Getting Started with AWS Firewall Manager to Enable AWS WAF Rules](getting-started-fms.md)\.

**Important**  
Firewall Manager does not support Amazon Route 53 or AWS Global Accelerator\. If you need to protect these resources with Shield Advanced, you can't use a Firewall Manager policy\. Instead, follow the instructions in [Adding AWS Shield Advanced Protection to More AWS Resources](configure-new-protection.md)\.

 To use Firewall Manager to enable Shield Advanced protection, perform the following steps in sequence\. 

**Topics**
+ [Step 1: Complete the Prerequisites](complete-prereq-fms-shield.md)
+ [Step 2: Create and Apply an AWS Firewall Manager Shield Advanced Policy](get-started-fms-shield-create-security-policy.md)
+ [Step 3: \(Optional\) Authorize the DDoS Response Team](get-started-fms-shield-authorize-DRT.md)
+ [Step 4: Configure Amazon SNS Notifications and Amazon CloudWatch Alarms](get-started-fms-shield-cloudwatch.md)
+ [Step 5: Deploy AWS WAF Rules](get-started-fms-shield-deploy-waf-automations.md)
+ [Step 6: Monitor the Global Threat Environment Dashboard](get-started-fms-shield-monitor-global-dashboard.md)