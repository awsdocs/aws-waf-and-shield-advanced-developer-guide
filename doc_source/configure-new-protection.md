# Adding AWS Shield Advanced protection to AWS resources<a name="configure-new-protection"></a>

As part of enabling Shield Advanced for an account, you optionally choose initial resources to protect\. You can add protection to more resources at any time\.

**Note**  
Shield Advanced protects only resources that you have specified either in Shield Advanced or through an AWS Firewall Manager Shield Advanced policy\. It doesn't automatically protect your resources\.

Shield Advanced offers advanced monitoring and protection for the following:
+ Elastic Load Balancing \(ELB\) load balancers
+ Amazon EC2 Elastic IP addresses
+ Amazon CloudFront distributions
+ Amazon Route 53 hosted zones
+ AWS Global Accelerator accelerators

You can monitor and protect up to 1,000 resources for each of these resource types per AWS account\. For example, you could protect 1,000 IP addresses, 1,000 distributions, and 1,000 load balancers in a single account\. If you want to increase the number of resources that you can protect, contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.

If you add resources after your initial setup, you typically must add Shield Advanced protection for each resource\. However, if you're using an AWS Firewall Manager Shield Advanced policy, you might not need to add resources yourself\. If a new resource is within the Firewall Manager policy scope, Firewall Manager automatically includes it within the Shield Advanced policy protection\.

**Important**  
Before you perform the following procedure, you must complete the procedure in [Step 1: Subscribe to AWS Shield Advanced](enable-ddos-prem.md)\.<a name="configure-new-protection-procedure"></a>

**To add protection for an AWS resource**

1. Sign in to the AWS Management Console and open the AWS WAF & Shield console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, under AWS Shield choose **Protected resources**\. 

1. Choose **Add resources to protect**\.

1. In the **Choose resources to protect with Shield Advanced** page, select the Regions and resource types that you want to protect, then choose **Load resources**\. 
**Note**  
If you want to protect an Amazon EC2 instance or a Network Load Balancer, you first must associate an Elastic IP address to it, and then choose the Elastic IP address as the resource to protect\.
If you choose an Elastic IP address as the resource to protect, Shield Advanced protects whatever resource is associated with that Elastic IP address\. Shield Advanced automatically identifies the type of resource that is associated with the Elastic IP address and applies the appropriate mitigations for that resource\. This includes configuring network ACLs that are specific to the Elastic IP address\. For more information about using Elastic IP addresses with your AWS resources, see the appropriate guide: [Amazon Elastic Compute Cloud Documentation](https://aws.amazon.com/documentation/ec2/) or [Elastic Load Balancing Documentation](https://aws.amazon.com/documentation/elastic-load-balancing/)\.
Shield Advanced does not support EC2\-Classic\.
Some scaling tools, like AWS Elastic Beanstalk, do not let you automatically attach an Elastic IP address to a Network Load Balancer\. For those cases, you need to manually associate the Elastic IP address\. 

1. Select the resources that you want to protect, then choose **Protect with Shield Advanced**\.

1. Walk through the options and provide the protection settings that you want to apply to the resource\. The options for adding protection to a resource are the same as for managing existing protections\. See [Configuring AWS Shield Advanced protections](manage-protection.md)\.