# Getting started with AWS Firewall Manager AWS Shield Advanced policies<a name="getting-started-fms-shield"></a>

You can use AWS Firewall Manager to enable AWS WAF rules, AWS WAF Classic rules, AWS Shield Advanced protections, and Amazon VPC security groups\. The steps for getting set up are slightly different for each:
+ To use Firewall Manager to enable AWS WAF rules, follow the steps in [Getting started with AWS Firewall Manager AWS WAF policies](getting-started-fms.md)\. 
+ To use Firewall Manager to enable Amazon VPC security groups, follow the steps in [Getting started with AWS Firewall Manager Amazon VPC security group policies](getting-started-fms-security-group.md)\. 
+ To use Firewall Manager to enable AWS WAF Classic rules, follow the steps in [Getting started with AWS Firewall Manager to enable AWS WAF Classic rules](classic-getting-started-fms.md)\. 

**Important**  
Firewall Manager does not support Amazon Route 53 or AWS Global Accelerator\. If you need to protect these resources with Shield Advanced, you can't use a Firewall Manager policy\. Instead, follow the instructions in [Adding AWS Shield Advanced protection to AWS resources](configure-new-protection.md)\.

 To use Firewall Manager to enable Shield Advanced protection, perform the following steps in sequence\. 

**Topics**
+ [Step 1: Complete the prerequisites](complete-prereq-fms-shield.md)
+ [Step 2: Create and apply an AWS Firewall Manager Shield Advanced policy](get-started-fms-shield-create-security-policy.md)
+ [Step 3: \(Optional\) authorize the DDoS Response Team \(DRT\)](get-started-fms-shield-authorize-DRT.md)
+ [Step 4: Configure Amazon SNS notifications and Amazon CloudWatch alarms](get-started-fms-shield-cloudwatch.md)
+ [Step 5: Monitor the global threat dashboard](get-started-fms-shield-monitor-global-dashboard.md)