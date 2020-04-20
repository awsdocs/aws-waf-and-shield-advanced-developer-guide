# Adding AWS Shield Advanced protection to AWS resources<a name="configure-new-protection"></a>

As part of enabling Shield Advanced for an account, you optionally choose initial resources to protect\. You can add protection to more resources at any time\. Shield Advanced offers advanced monitoring and protection for the following:
+ Elastic IP addresses
+ Amazon CloudFront distributions
+ Amazon Route 53 hosted zones
+ Elastic Load Balancing load balancers
+ AWS Global Accelerator accelerators

You can monitor and protect up to 1,000 resources for each of these resource types per AWS account\. For example, you could protect 1,000 IP addresses, 1,000 distributions, and 1,000 load balancers in a single account\. If you want to increase the number of resources that you can protect, contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.

If you are using an AWS Firewall Manager Shield Advanced policy, you don't need to add resources using the procedure in this section\. If the resource is within the Firewall Manager policy scope, that is, the resource is of the correct type and has the correct tags as defined by the policy, Firewall Manager automatically includes it within its protection\. 

**Important**  
Before you perform the following procedure, you must complete the procedure in [Step 1: Activate AWS Shield Advanced](enable-ddos-prem.md)\.<a name="configure-new-protection-procedure"></a>

**To add protection for an AWS resource**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, under AWS Shield choose **Protected resources**\. 

1. Choose **Add protected resources**\.

1. Choose or enter the resource types and resources to protect\. For Classic Load Balancer and Application Load Balancer resources, you also must choose a Region\. 

   You can choose from the provided list or enter the Amazon Resource Name \(ARN\) of specific resources to protect\. You can choose or enter any combination of resource types and resources\. 

   Shield Advanced lists a maximum of 100 resources at one time\. If you have more than 100 resources, choose **Next** to see the next set\.

   If you want to protect an Amazon EC2 instance, you must first associate an Elastic IP address with the instance, and then choose the Elastic IP address as the resource to protect\.
**Note**  
Shield Advanced does not support EC2\-Classic\.
**Note**  
If you choose an Elastic IP address as the resource to protect, Shield Advanced protects whatever resource is associated with that Elastic IP address, either an Amazon EC2 instance or an Elastic Load Balancing load balancer\. Shield Advanced automatically identifies the type of resource associated with the Elastic IP address and applies the appropriate mitigations for that resource, including configuring network ACLs specific to that Elastic IP address\. For more information about using Elastic IP addresses with your AWS resources, see the appropriate guide: [Amazon Elastic Compute Cloud Documentation](https://aws.amazon.com/documentation/ec2/) or [Elastic Load Balancing Documentation](https://aws.amazon.com/documentation/elastic-load-balancing/)\. Shield Advanced does not support EC2\-Classic\.

1. Choose **Protect selected resources**\.

1. Walk through the options and provide the protection settings that you want to apply to the resource\. The options for adding protection to a resource are the same as for managing existing protections\. See [Managing AWS Shield Advanced protections](manage-protection.md)\.