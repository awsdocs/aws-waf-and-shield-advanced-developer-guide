# Subscribe to AWS Shield Advanced<a name="enable-ddos-prem"></a>

You must subscribe to Shield Advanced for each AWS account that you want to protect\. 

For accounts that are members of an AWS Organizations organization, AWS bills Shield Advanced subscriptions against the organization's payer account, regardless of whether the payer account itself is subscribed\. 

**Subscribing multiple accounts**  
When you subscribe multiple accounts that are in the same [AWS Organizations consolidated billing account family](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/consolidated-billing.html), one subscription price covers all subscribed accounts in the family\. The organization must own all of the AWS accounts and their resources\. Exceptions apply for AWS Channel Resellers\. For detailed pricing information and examples, see [AWS Shield Advanced Pricing](http://aws.amazon.com/shield/pricing/)\.

If your accounts are part of an organization, we recommend that you use AWS Firewall Manager if you can, to automate your subscriptions and protections for the organization\. Firewall Manager supports all protected resource types except for Amazon Route 53 and AWS Global Accelerator\. To use Firewall Manager, see [AWS Firewall Manager](fms-chapter.md) and [Getting started with AWS Firewall Manager​ AWS Shield Advanced policiesGetting started with AWS Shield Advanced policies](getting-started-fms-shield.md)\. 

If you don't use Firewall Manager, for each account with resources to protect, subscribe and add protections using the following procedures\. 

**To subscribe an account to AWS Shield Advanced**

1. Sign in to the AWS Management Console and open the AWS WAF & Shield console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the **AWS Shield** navigation bar, choose **Getting started**\. Choose **Subscribe to Shield Advanced**\. 

1. In the **Subscribe to Shield Advanced** page, read each term of the agreement, and then select all of the check boxes to indicate that you accept the terms\. For accounts in a consolidated billing family, you must agree to the terms for each account\. 
**Important**  
When you are subscribed, to unsubscribe you must contact [AWS Support](https://console.aws.amazon.com/support)\.   
To disable autorenewal for your subscription, you must use the Shield API operation [UpdateSubscription](https://docs.aws.amazon.com/waf/latest/DDOSAPIReference/API_UpdateSubscription.html) or the CLI command [update\-subscription](https://docs.aws.amazon.com/cli/latest/reference/shield/update-subscription.html)\.

   Choose **Subscribe to Shield Advanced**\. This subscribes your account to Shield Advanced and activates the service\.

Your account is subscribed\. Continue through the following steps to protect your account's resources with Shield Advanced\. 

**Note**  
Shield Advanced doesn't automatically protect your resources after you subscribe\. You must specify the resources you want Shield Advanced to protect configure the protections\. 