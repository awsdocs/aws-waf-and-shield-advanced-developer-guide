# Step 3: Authorize the DDoS Response Team to Create Rules and Web ACLs on Your Behalf<a name="authorize-DRT"></a>

One of the benefits of AWS Shield Advanced is support from the DDoS response team \(DRT\)\. When you experience a potential DDoS attack, you can contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\. If necessary, the Support Center escalates your issue to the DRT\. The DRT can help you analyze the suspicious activity and assist you in mitigating the issue\. This mitigation often involves creating or updating AWS WAF rules and web access control lists \(web ACLs\) in your account\. The DRT can inspect your AWS WAF configuration and create or update AWS WAF rules and web ACLs for you, but the team needs your authorization to do so\. We recommend that as part of enabling AWS Shield Advanced, you proactively provide the DRT with the needed authorization\. Providing authorization ahead of time helps prevent mitigation delays in the event of an actual attack\. 

To authorize the DRT to inspect your AWS WAF configuration and create and update AWS WAF rules and web ACLs on your behalf, you must use an AWS CloudFormation template that creates a cross\-account IAM role\. This role establishes a trust relationship with the DRT support account and applies a policy giving the DRT full access to your AWS WAF resources\. The policy enables the DRT to inspect your AWS WAF configuration and create or update AWS WAF rules and web ACLs\. 

The policy gives the DRT access only to your AWS WAF and Shield resources\. By running this template, you authorize the DRT to inspect your AWS WAF and Shield configuration and create and update AWS WAF rules and web ACLs on your behalf\. The DRT takes these actions only if explicitly authorized by you, as described on this page\. 

**Important**  
You must complete [Step 1: Enable and Configure AWS Shield Advanced](enable-ddos-prem.md) and [Step 2: Add AWS Shield Advanced Protection to more AWS Resources](configure-new-protection.md) before you start this procedure\.<a name="authorize-DRT-procedure"></a>

**To authorize the DRT to mitigate potential attacks on your behalf**

1. Use this link to create an AWS CloudFormation stack: [AWS CloudFormation DRT stack](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#cstack=sn%7eRateBasedBL%7cturl%7ehttps:%2f%2fs3.amazonaws.com/aws-shield-drt-support/drt_support_iam_role.json)\. The link pre\-populates the AWS CloudFormation **Select Template** page with the correct AWS CloudFormation template name\.

1. Choose **Next**\. 

1. For **Stack name**, type a name, and then choose **Next**\. 

1. On the **Options** page, keep the defaults, and then choose **Next**\.

1. Review the summary, and then choose **Create**\.

After you authorize the DRT to act on your behalf, you should go to [Step 4: Create a DDoS Dashboard in CloudWatch and set CloudWatch alarms ](deploy-waf-dashboard.md)\.