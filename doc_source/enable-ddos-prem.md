# Step 1: Subscribe to AWS Shield Advanced<a name="enable-ddos-prem"></a>

AWS Shield Advanced provides advanced DDoS detection and mitigation protection for network layer \(layer 3\), transport layer \(layer 4\), and application layer \(layer 7\) attacks\.

**Important**  
Activate Shield Advanced for each AWS account that you want to protect\. If you want to activate Shield Advanced for multiple accounts, we recommend that you use AWS Firewall Manager if you can\. Firewall Manager doesn't support Amazon Route 53 or AWS Global Accelerator accelerator, but it supports the other resource types\. For more information, see [Getting started with AWS Firewall Manager AWS Shield Advanced policies](getting-started-fms-shield.md)\. 

**Note**  
The console guidance provided here is for the latest version of the AWS Shield console, released in 2020\. In the console, you can switch between versions\. <a name="enable-ddos-prem-procedure"></a>

**To subscribe to AWS Shield Advanced**

1. Sign in to the AWS Management Console and open the AWS WAF & Shield console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the **AWS Shield** navigation bar, choose **Getting started**\. Choose **Subscribe to Shield Advanced**\. 

1. In the **Subscribe to Shield Advanced** page, read each term of the agreement, and then select all of the check boxes to indicate that you accept the terms\. 
**Important**  
By choosing **Subscribe to Shield Advanced**, you subscribe to Shield Advanced and activate the service\. To unsubscribe, you must contact [AWS Support](https://console.aws.amazon.com/support)\. 

   Choose **Subscribe to Shield Advanced**\.

## Using AWS Shield Advanced with multiple accounts<a name="enable-ddos-prem-multi-account-procedure"></a>

You must activate Shield Advanced for each AWS account that you want to protect\. To activate Shield Advanced for multiple accounts, we recommend that you use AWS Firewall Manager if you can\. Firewall Manager doesn't support Amazon Route 53 or AWS Global Accelerator accelerator, but it supports the other resource types\. For more information, see [Getting started with AWS Firewall Manager AWS Shield Advanced policies](getting-started-fms-shield.md)\. Alternatively, for each account, log into the console and follow the procedure [To subscribe to AWS Shield Advanced](#enable-ddos-prem-procedure)\. 

If you activate Shield Advanced for multiple accounts that are in the same [consolidated billing account family](http://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/consolidated-billing.html), the monthly subscription fee covers all those accounts\. You don't pay extra subscription fees for individual accounts\. You must own all the AWS accounts and resources in the account\. 

**Note**  
AWS Channel resellers pay a separate monthly fee for each member account\. AWS Channel resellers who resell AWS Shield Advanced to customers with more than one member account can [contact us](https://aws.amazon.com/contact-us/) for additional billing support\. With respect to such AWS Channel resellers, AWS reserves the right to modify the monthly fee for AWS Shield Advanced\. For more information, see the [AWS Shield Advanced Pricing](http://aws.amazon.com/shield/pricing/) page\. 

The first time that you activate Shield Advanced from an account, you are presented with a pricing agreement\. The pricing agreement is displayed on the console each time that you activate Shield Advanced from a different account\. The pricing agreement covers all activated accounts in a consolidated billing family, but you must agree to the terms each time that you activate an account\. 

You can now go to [Step 2: Add resources to protect](ddos-choose-resources.md)\. 