# Step 2: Add AWS Shield Advanced Protection to AWS Resources<a name="configure-new-protection"></a>

As part of enabling Shield Advanced for an account, you choose an initial resource to protect\. You likely will want to add protection to more resources\. Shield Advanced offers advanced monitoring and protection for up to 100 resources that include any combination of CloudFront distributions, Amazon Route 53 hosted zones, or Elastic Load Balancing resources\. If you want to increase these limits, contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.

**Important**  
You must complete [Step 1: Enable and Configure AWS Shield Advanced](enable-ddos-prem.md) before you start Step 2\.

**To add protection for an AWS resource**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/waf/](https://console.aws.amazon.com/waf/)\. 

1. Choose **Protected resources**\. 

1. Choose **Add DDoS protection**\.

1. Choose the resource type and resource to protect\. For Classic Load Balancer and Application Load Balancer resources, you also must choose a region\.

1. For **Name**, type a friendly name to help you identify the AWS resources that are protected\. For example, **My CloudFront AWS Shield Advanced distributions**\.

1. \(Optional\) For **Web DDoS attack**, select **Enable**\. You are prompted to associate an existing web ACL with these resources, or create a web ACL if you don't have one yet\.

   You can disable this protection later by following the steps described in [Removing AWS Shield Advanced from an AWS Resource](remove-protection.md)\.

1. Choose **Add DDoS protection**\.

After you have added DDoS protection to all the appropriate resources, go to [Step 3: Authorize the DDoS Response Team to Create Rules and Web ACLs on Your Behalf](authorize-DRT.md)\.