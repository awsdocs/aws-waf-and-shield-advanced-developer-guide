# Step 1: Activate AWS Shield Advanced<a name="enable-ddos-prem"></a>

AWS Shield Advanced provides advanced DDoS detection and mitigation protection for network layer \(layer 3\), transport layer \(layer 4\), and application layer \(layer 7\) attacks\.

**Important**  
You must activate Shield Advanced for each AWS account that you want to protect\. If you want to activate Shield Advanced for multiple accounts, we recommend that you use AWS Firewall Manager\. For more information, see [Getting started with AWS Firewall Manager AWS Shield Advanced policies](getting-started-fms-shield.md)\. <a name="enable-ddos-prem-procedure"></a>

**To activate AWS Shield Advanced**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. If this is your first time signing in to the AWS WAF console, choose **Go to Shield**, and then choose **Activate AWS Shield Advanced**\. Read each term of the agreement, and then select each check box to indicate that you accept the terms\. Before you can continue, you must select all check boxes, then choose **Activate service**\.
**Important**  
By choosing **Activate service**, you are subscribing to Shield Advanced and activating the service\. To unsubscribe, contact [AWS Support](https://console.aws.amazon.com/support)\. 

   Otherwise, in the navigation pane, under **AWS Shield**, choose **Protected resources**\. 

You can now go to [Step 2: Specify your resources to protect](ddos-choose-resources.md)\. 

## Activating and setting up AWS Shield Advanced for multiple accounts<a name="enable-ddos-prem-multi-account-procedure"></a>

You must activate Shield Advanced for each AWS account that you want to protect\. To activate Shield Advanced for multiple accounts, we recommend that you use AWS Firewall Manager\. For more information, see [Getting started with AWS Firewall Manager AWS Shield Advanced policies](getting-started-fms-shield.md)\. Alternatively, you can follow the procedure in [Step 1: Activate AWS Shield Advanced](#enable-ddos-prem) for each account, each time logging in with a different account\. 

If you activate Shield Advanced for multiple accounts that are in the same [consolidated billing account family](http://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/consolidated-billing.html), the monthly subscription fee covers all those accounts\. You don't pay extra subscription fees for individual accounts\. You must own all the AWS accounts and resources in the account\. 

**Note**  
AWS Channel Resellers pay a separate monthly fee for each member account\. AWS Channel Resellers who resell AWS Shield Advanced to customers with more than one member account can [contact us](https://aws.amazon.com/contact-us/) for additional billing support\. With respect to such AWS Channel Resellers, AWS reserves the right to modify the monthly fee for AWS Shield Advanced\. For more information, see the [AWS Shield Advanced Pricing](http://aws.amazon.com/shield/pricing/) page\. 

The first time that you activate Shield Advanced from an account, you are presented with a pricing agreement\. The pricing agreement is displayed on the console each time that you activate Shield Advanced from a different account\. The pricing agreement covers all activated accounts in a consolidated billing family, but you must agree to the terms each time that you activate an account\. 

You can now go to [Step 2: Specify your resources to protect](ddos-choose-resources.md)\.