# Configuring access for the Shield Response Team \(SRT\)<a name="ddos-srt-access"></a>

You can grant permission to the Shield Response Team \(SRT\) to act on your behalf, accessing your AWS WAF logs and making calls to the AWS Shield Advanced and AWS WAF APIs to manage protections\. During application layer DDoS events, the SRT can monitor AWS WAF requests to identify anomalous traffic and help craft custom AWS WAF rules to mitigate offending traffic sources\. 

Additionally, you can grant the SRT access to other data that you have stored in Amazon S3 buckets, such as packet captures or logs from an Application Load Balancer, Amazon CloudFront, or from third party sources\.

**Note**  
To use the services of the Shield Response Team \(SRT\), you must be subscribed to the [Business Support plan](https://aws.amazon.com/premiumsupport/business-support/) or the [Enterprise Support plan](https://aws.amazon.com/premiumsupport/enterprise-support/)\. 

**To manage permissions for the SRT**

1. In the AWS Shield console **Overview** page, under **Configure AWS SRT support**, choose **Edit SRT access**\. The **Edit AWS Shield Response Team \(SRT\) access** page opens\.

1. For **SRT access setting** select one of the options: 
   + **Do not grant the SRT access to my account** – Shield removes any permissions you previously gave to the SRT to access your account and resources\.
   + **Create a new role for the SRT to access my account** – Shield creates a role that trusts the service principal `drt.shield.amazonaws.com`, which represents the SRT, and attaches the managed policy `AWSShieldDRTAccessPolicy` to it\. The managed policy allows the SRT to make AWS Shield Advanced and AWS WAF API calls on your behalf and to access your AWS WAF logs\. For more information about the managed policy, see [AWS managed policy: AWSShieldDRTAccessPolicy](shd-security-iam-awsmanpol.md#shd-security-iam-awsmanpol-AWSShieldDRTAccessPolicy)\.
   + **Choose an existing role for the SRT to access my accounts** – For this option, you must modify the configuration of the role in AWS Identity and Access Management \(IAM\) as follows: 
     + Attach the managed policy `AWSShieldDRTAccessPolicy` to the role\. This managed policy allows the SRT to make AWS Shield Advanced and AWS WAF API calls on your behalf and to access your AWS WAF logs\. For more information about the managed policy, see [AWS managed policy: AWSShieldDRTAccessPolicy](shd-security-iam-awsmanpol.md#shd-security-iam-awsmanpol-AWSShieldDRTAccessPolicy)\. For information about attaching the managed policy to your role, see [Attaching and Detaching IAM Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_manage-attach-detach.html)\. 
     + Modify the role to trust the service principal `drt.shield.amazonaws.com`\. This is the service principal that represents the SRT\. For more information, see [IAM JSON Policy Elements: Principal](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_principal.html)\. 

1. For **\(Optional\): Grant SRT access to an Amazon S3 bucket**, if you need to share data that isn't in your AWS WAF web ACL logs, configure this\. For example, Application Load Balancer access logs, Amazon CloudFront logs, or logs from third party sources\. 
**Note**  
You don't need to do this for your AWS WAF web ACL logs\. The SRT gains access to those when you grant access to your account\. 

   1. Configure the Amazon S3 buckets according to the following guidelines: 
      + The bucket locations must be in the same AWS account as the one you gave the SRT general access to, in the prior step **AWS Shield Response Team \(SRT\) access**\. 
      + The buckets can be either plaintext or SSE\-S3 encrypted\. For more information about Amazon S3 SSE\-S3 encryption, see [Protecting Data Using Server\-Side Encryption with Amazon S3\-Managed Encryption Keys \(SSE\-S3\)](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html) in the Amazon S3 User Guide\.

        The SRT cannot view or process logs that are stored in buckets that are encrypted with keys stored in AWS Key Management Service \(AWS KMS\)\. 

   1. In the Shield Advanced **\(Optional\): Grant SRT access to an Amazon S3 bucket** section, for each Amazon S3 bucket where your data or logs are stored, enter the name of the bucket and choose **Add Bucket**\. You can add up to 10 buckets\.

      This grants the SRT the following permissions on each bucket: `s3:GetBucketLocation`, `s3:GetObject`, and `s3:ListBucket`\.

      If you want to give the SRT permission to access more than 10 buckets, you can do this by editing the additional bucket policies and manually granting the permissions listed here for the SRT\.

1. Choose **Save** to save your changes\.

You can also authorize the SRT through the API by creating an IAM role, attaching the policy AWSShieldDRTAccessPolicy to it, and then passing the role to the operation [AssociateDRTRole](https://docs.aws.amazon.com/waf/latest/DDOSAPIReference/API_AssociateDRTRole.html)\. 