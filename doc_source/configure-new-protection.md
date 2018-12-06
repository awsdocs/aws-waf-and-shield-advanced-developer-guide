# Add AWS Shield Advanced Protection to more AWS Resources<a name="configure-new-protection"></a>

As part of enabling Shield Advanced for an account, you choose initial resources to protect\. You might want to add protection to more resources\. Shield Advanced offers advanced monitoring and protection for up to 100 resources that include any combination of Elastic IP addresses, Amazon CloudFront distributions, Amazon Route 53 hosted zones, Elastic Load Balancing resources or your AWS Global Accelerator accelerators\. If you want to increase these limits, contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.

**Important**  
You must complete [Step 1: Activate AWS Shield Advanced](enable-ddos-prem.md) before you perform this procedure\.<a name="configure-new-protection-procedure"></a>

**To add protection for an AWS resource**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/waf/](https://console.aws.amazon.com/waf/)\. 

1. Choose **Protected resources**\. 

1. Choose **Add protected resources**\.

1. Choose or enter the resource types and resources to protect\. For Classic Load Balancer and Application Load Balancer resources, you also must choose a region\. 

   You can choose from the provided list or enter the Amazon Resource Name \(ARN\) of specific resources to protect\. You can choose or enter any combination of resource types and resources\. 

   Shield Advanced lists a maximum of 100 resources at one time\. If you have more than 100 resources, choose **Next** to see the next set\.

   If you want to protect an Amazon EC2 instance, you must first associate an Elastic IP address to the instance, then choose the Elastic IP address as the resource to protect\.
**Note**  
Shield Advanced does not support EC2\-Classic\.

1. Choose **Protect selected resources**\.

1. Add a web ACL and rate\-based rule as described in the Getting Started section, [Step 3: Add Rate\-based Rules](ddos-get-started-rate-based-rules.md)\.

1. Configure a CloudWatch alarm as described in the Getting Started section, [Step 5: Configure Amazon CloudWatch Alarms](ddos-get-started-cloudwatch.md)\.

**Note**  
If you choose an Elastic IP address as the resource to protect, Shield Advanced will protect whatever resource is associated with that Elastic IP address, either an Amazon EC2 instance or an Elastic Load Balancing load balancer\. Shield Advanced automatically identifies the type of resource associated with the Elastic IP address and applies the appropriate mitigations for that resource, including configuring network ACLs specific to that Elastic IP address\. For more information on using Elastic IP addresses with your AWS resources, see the appropriate guide: [Amazon Elastic Compute Cloud Documentation](https://aws.amazon.com/documentation/ec2/) or [Elastic Load Balancing Documentation](https://aws.amazon.com/documentation/elastic-load-balancing/)\. Shield Advanced does not support EC2\-Classic\.