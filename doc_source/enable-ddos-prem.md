# Subscribe to AWS Shield Advanced<a name="enable-ddos-prem"></a>

You must subscribe to Shield Advanced for each AWS account that you want to protect\. 

**Note**  
For accounts that are members of an AWS Organizations organization, Shield Advanced subscriptions are billed against the organization's payer account, regardless of whether the payer account itself is subscribed\. 

If you want to subscribe multiple accounts, do one of the following: 
+ Use AWS Firewall Manager if you can\. Firewall Manager doesn't support Amazon Route 53 or AWS Global Accelerator, but it supports the other resource types that Shield Advanced protects\. For more information about Firewall Manager, see [Getting started with AWS Firewall Manager​ AWS Shield Advanced policies](getting-started-fms-shield.md)\. 
+ If you can't use Firewall Manager, for each account, log into the console and subscribe as described in the following procedure\. 

**To subscribe to AWS Shield Advanced**

1. Sign in to the AWS Management Console and open the AWS WAF & Shield console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the **AWS Shield** navigation bar, choose **Getting started**\. Choose **Subscribe to Shield Advanced**\. 

1. In the **Subscribe to Shield Advanced** page, read each term of the agreement, and then select all of the check boxes to indicate that you accept the terms\. 
**Important**  
By choosing **Subscribe to Shield Advanced**, you subscribe to Shield Advanced and activate the service\. To unsubscribe, you must contact [AWS Support](https://console.aws.amazon.com/support)\. 

   Choose **Subscribe to Shield Advanced**\.

**Note**  
Shield Advanced doesn't automatically protect your resources\. It protects only resources that you have specified either in Shield Advanced or in a Firewall Manager Shield Advanced policy\. 

After you subscribe to Shield Advanced, you must specify the resources that you want to protect with Shield Advanced\. You can do this in the following step or after your initial configuration, using the procedure at [Adding AWS Shield Advanced protection to AWS resources](ddos-manage-protected-resources.md#configure-new-protection) \. 

## Using AWS Shield Advanced with multiple accounts<a name="enable-ddos-prem-multi-account-procedure"></a>

You must subscribe to Shield Advanced for each AWS account that you want to protect\. To subscribe multiple accounts, we recommend that you use AWS Firewall Manager, if you can\. Firewall Manager doesn't support Amazon Route 53 or AWS Global Accelerator, but it supports the other resource types\. For more information, see [Getting started with AWS Firewall Manager​ AWS Shield Advanced policies](getting-started-fms-shield.md)\. Alternatively, for each account, log into the console and follow the preceding procedure [Subscribe to AWS Shield Advanced](#enable-ddos-prem)\. 

If you subscribe multiple accounts that are in the same [consolidated billing account family](http://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/consolidated-billing.html), the monthly subscription fee covers all those accounts\. You don't pay extra subscription fees for individual accounts\. You must own all of the AWS accounts and resources in the account\. 

**Note**  
AWS Channel resellers pay a separate monthly fee for each member account\. AWS Channel resellers who resell AWS Shield Advanced to customers with more than one member account can [contact us](https://aws.amazon.com/contact-us/) for additional billing support\. With respect to such AWS Channel resellers, AWS reserves the right to modify the monthly fee for AWS Shield Advanced\. For more information, see [AWS Shield Advanced Pricing](http://aws.amazon.com/shield/pricing/)\. 

The first time that you subscribe to Shield Advanced from an account, you are presented with a pricing agreement\. The pricing agreement is displayed on the console each time that you subscribe using a different account\. This agreement covers all subscribed accounts in a consolidated billing family, but you must agree to the terms for each account\. 