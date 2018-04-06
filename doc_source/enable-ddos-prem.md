# Step 1: Enable and Configure AWS Shield Advanced<a name="enable-ddos-prem"></a>

AWS Shield Advanced provides advanced DDoS detection and mitigation protection for network layer \(layer 3\), transport layer \(layer 4\), and application layer \(layer 7\) attacks\.

**Important**  
You must enable Shield Advanced for each AWS account that you want to protect\. For more information, see Enabling and Configuring AWS Shield Advanced for Multiple Accounts\.<a name="enable-ddos-prem-procedure"></a>

**To enable and configure AWS Shield Advanced**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/waf/](https://console.aws.amazon.com/waf/)\. 

1. If this is your first time logging in to the AWS WAF console, choose **Go to AWS Shield Advanced**\. Otherwise, choose **Protected resources**\. 

1. If this is your first time logging in to the AWS Shield Advanced console, choose **Activate AWS Shield Advanced** and then accept the AWS Shield Advanced pricing agreement\. Otherwise choose **Add protected resource**\.

1. Choose or enter the resource types and resources to protect\. For Classic Load Balancer and Application Load Balancer resources, you also must choose a region\. 

   You can choose from the provided list or enter the Amazon Resource Name \(ARN\) of specific resources to protect\. You can choose or enter any combination of resource types and resources\. 

   Shield Advanced lists a maximum of 100 resources at one time\. If you have more than 100 resources, choose **Next** to see the next set\.

   If you want to protect an Amazon EC2 instance, you must first associate an Elastic IP address to the instance, then choose the Elastic IP address as the resource to protect\.
**Note**  
Shield Advanced does not support EC2\-Classic\.

1. For **Name**, enter a friendly name to help you identify the AWS resources that are protected\. For example, **My CloudFront AWS Shield Advanced distributions**\.

1. \(Optional\) For **Web DDoS attack**, select **Enable**\. You are prompted to associate an existing web ACL with these resources, or create a web ACL if you don't have one yet\.

   You can disable this protection later by following the steps described in [Removing AWS Shield Advanced from an AWS Resource](remove-protection.md)\.

1. Choose **Add DDoS protection**\.

To protect additional resources, see [Step 2: Add AWS Shield Advanced Protection to more AWS Resources](configure-new-protection.md)\.

**Note**  
If you choose an Elastic IP address as the resource to protect, Shield Advanced will protect whatever resource is associated with that Elastic IP address, either an Amazon EC2 instance or an Elastic Load Balancing load balancer\. Shield Advanced automatically identifies the type of resource associated with the Elastic IP address and applies the appropriate mitigations for that resource, including configuring network ACLs specific to that Elastic IP address\. For more information on using Elastic IP addresses with your AWS resources, see the appropriate guide: [Amazon Elastic Compute Cloud Documentation](https://aws.amazon.com/documentation/ec2/) or [Elastic Load Balancing Documentation](https://aws.amazon.com/documentation/elastic-load-balancing/)\. Shield Advanced does not support EC2\-Classic\.

## Enabling and Configuring AWS Shield Advanced for Multiple Accounts<a name="enable-ddos-prem-multi-account-procedure"></a>

You must enable Shield Advanced for each AWS account that you want to protect\. To do so, follow the procedure in Enable and Configure Shield Advanced for each account, each time logging in with a different account\. 

The first time that you enable Shield Advanced from an account, you are presented with a pricing agreement\. The AWS Shield Advanced fee applies for each business that is subscribed to AWS Shield Advanced\. So although the pricing agreement displays in the console each time that you enable Shield Advanced from a new account, if your business has multiple AWS accounts, you pay just one Shield Advanced monthly fee as long as all the AWS accounts are in the same [Consolidated Billing account family](http://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/consolidated-billing.html)\. Further, you must own all the AWS accounts and resources in the account\.