# Step 1: Enable and Configure AWS Shield Advanced<a name="enable-ddos-prem"></a>

AWS Shield Advanced provides advanced DDoS detection and mitigation protection for network layer \(layer 3\), transport layer \(layer 4\), and application layer \(layer 7\) attacks\.

**Important**  
You must enable Shield Advanced for each AWS account that you want to protect\. For more information, see Enabling and Configuring AWS Shield Advanced for Multiple Accounts\.

**To enable and configure AWS Shield Advanced**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/waf/](https://console.aws.amazon.com/waf/)\. 

1. If this is your first time logging in to the AWS WAF console, choose **Get started with AWS Shield Advanced**\. Otherwise, choose **Protected resources**\. 

1. Choose **Activate AWS Shield Advanced**\.

1. Choose the resource type and resource to protect\.

1. For **Name**, enter a friendly name to help you identify the AWS resources that are protected\. For example, **My CloudFront AWS Shield Advanced distributions**\.

1. \(Optional\) For **Web DDoS attack**, select **Enable**\. You are prompted to associate an existing web ACL with these resources, or create a web ACL if you don't have one yet\.

   You can disable this protection later by following the steps described in [Removing AWS Shield Advanced from an AWS Resource](remove-protection.md)\.

1. Choose **Add DDoS protection**\.

To protect additional resources, see [Step 2: Add AWS Shield Advanced Protection to AWS Resources](configure-new-protection.md)\.

## Enabling and Configuring AWS Shield Advanced for Multiple Accounts<a name="enable-ddos-prem-multi-account-procedure"></a>

You must enable Shield Advanced for each AWS account that you want to protect\. To do so, follow the procedure in Enable and Configure Shield Advanced for each account, each time logging in with a different account\. 

The first time that you enable Shield Advanced from an account, you are presented with a pricing agreement\. The AWS Shield Advanced fee applies for each business that is subscribed to AWS Shield Advanced\. So although the pricing agreement displays in the console each time that you enable Shield Advanced from a new account, if your business has multiple AWS accounts, you pay just one Shield Advanced monthly fee as long as all the AWS accounts are in the same [Consolidated Billing account family](http://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/consolidated-billing.html)\. Further, you must own all the AWS accounts and resources in the account\.