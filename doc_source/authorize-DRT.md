# Step 5: Configure AWS SRT support<a name="authorize-DRT"></a>

With AWS Shield Advanced, you can engage with the AWS Shield Response Team \(SRT\) if your application is unhealthy because of a possible DDoS attack\. 

**Note**  
To contact the SRT, you must be subscribed to the [Business Support plan](https://aws.amazon.com/premiumsupport/business-support/) or the [Enterprise Support plan](https://aws.amazon.com/premiumsupport/enterprise-support/)\. If you are not subscribed to either plan, some of the options described in this section might not be visible in your account or accessible via the AWS Shield Advanced API\.

You can contact the Shield Response Team \(SRT\) in one of the following ways: 
+ **Support case** – You can open a case under **AWS Shield** in the [AWS Support Center](https://docs.aws.amazon.com/awssupport/latest/user/case-management.html)\. If your application is unhealthy, open a case using the highest severity available for your support plan and select either the **Phone** or **Chat** contact options\. In the description for your case, provide as much detail as possible\. Be sure to provide information about any protected resources that you think might be affected, and the current state of your end\-user experience\. For example, if your user experience is degraded or parts of your application are currently unavailable, provide that information\. 
+ **Proactive engagement** – With AWS Shield Advanced proactive engagement, the SRT contacts you directly if the Amazon Route 53 health check associated with your protected resource becomes unhealthy during an event that is detected by Shield Advanced\. For more information about this option, see [Shield Advanced proactive engagement](ddos-overview.md#ddos-advanced-proactive-engagement)\.

**Grant the SRT limited access to certain APIs and Amazon S3 buckets that you designate**

AWS Shield Advanced automatically mitigates DDoS attacks against your resources\. Shield Advanced detects web application layer vectors, like web request floods and low\-and\-slow bad bots, but does not automatically mitigate them\. To mitigate web application layer vectors, you must employ AWS WAF rules or the SRT must employ the rules on your behalf\. 

**Note**  
Shield Advanced detects web application layer events when you protect Amazon CloudFront distributions and Application Load Balancers\. These events indicate a statistically significant deviation in traffic, compared to your application’s historical baseline\. You can choose to take no action if a deviation is expected or has not affected the health of your resource\.

The SRT can assist you with web application layer events if you grant limited access to your Shield Advanced and AWS WAF APIs\. You can revoke access at any time\. The SRT engineers only access your APIs with your authorization, limited to the scope of your support engagement\. 

**\(Optional\) Grant SRT access to an Amazon S3 bucket**

To mitigate application layer events you can share additional log data, such as Application Load Balancer access logs, Amazon CloudFront logs, or logs from third party sources\. For the SRT to view or process your logs, they must be in Amazon S3 buckets that satisfy the following requirements:

**To authorize the SRT to assist with web application layer events on your behalf**

1. 
   + The buckets must be managed in one of the following ways:
     + \(Option\) The buckets are in the same AWS account as the web ACL\. 
     + \(Option\) The buckets are located in a separate account, and you have ensured that the SRT can access them\. If you have multiple accounts in your organization, you can use a central Amazon S3 bucket in any of your Shield Advanced accounts within the organization\. Alternately, you can use an Amazon S3 bucket in an account that does not have Shield Advanced providing it stores logs for an AWS WAF web ACL that is associated with a Shield Advanced protected resource\. 
     + \(Option\) The buckets are the storage destination for logging that is managed by AWS Firewall Manager for an AWS WAF policy\. 
   + The buckets can be either plaintext  or SSE\-S3 encrypted\. For more information about Amazon S3 SSE\-S3 encryption, see [Protecting Data Using Server\-Side Encryption with Amazon S3\-Managed Encryption Keys \(SSE\-S3\)](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html) in the [Amazon Simple Storage Service Amazon Simple Storage Service Developer Guide](https://docs.aws.amazon.com/AmazonS3/latest/dev/Welcome.html)\.

     The SRT cannot view or process logs that are stored in buckets that are encrypted with keys stored in AWS Key Management Service \(AWS KMS\)\. 
   + Shield Advanced allows you to give the SRT permission to access up to 10 buckets\. If you want to give permission to more than 10, you need to edit the bucket policies manually\.

1. In the AWS Shield console **Overview** page, under **Configure AWS SRT support**, choose **Edit SRT access**\.

1. For the **SRT access setting**, select one of the following: 
   + \(Option\) **Create a new role for the SRT to access my account** – For this option, Shield creates the role and automatically configures it for use\. The new role allows the SRT to access your AWS Shield Advanced and AWS WAF resources\. It also trusts the service principal `drt.shield.amazonaws.com`, which represents the SRT\.
   + \(Option\)  **Choose an existing role for the SRT to access my account** – For this option, you must modify the configuration of the role in AWS Identity and Access Management \(IAM\) as follows: 
     + Attach the managed policy `AWSShieldDRTAccessPolicy` to the role\. The `AWSShieldDRTAccessPolicy` managed policy gives the SRT access to your AWS Shield Advanced and AWS WAF resources\. For more information, see [Attaching and Detaching IAM Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_manage-attach-detach.html)\. 
     + Modify the role to trust the service principal `drt.shield.amazonaws.com`\. This is the service principal that represents the SRT\. For more information, see [IAM JSON Policy Elements: Principal](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_principal.html)\. 

1. For each Amazon S3 bucket where your data or logs are stored, enter the name of the bucket and choose **Add Bucket**\. You can add up to 10 buckets\.

   This grants the SRT the following permissions on the bucket: `s3:GetBucketLocation`, `s3:GetObject`, and `s3:ListBucket`\.

   If you want to give the SRT permission to access more than 10 buckets, you can do this by editing the additional bucket policies manually\.

1. Choose **Save**\.

**To enable SRT proactive engagement**

Shield Advanced proactive engagement allows you to engage with the SRT more quickly when the availability of your application is affected, because of a possible attack\. When you have proactive engagement enabled, the SRT contacts you when a Shield Advanced event correlates to an unhealthy Route 53 health check on one or more of your protected resources\.

1. In the AWS Shield console **Overview** page, under **Proactive engagement and contacts**, in the contacts area, choose **Edit**\.

   In the **Edit contacts** page, provide the contact information for the people that you want the SRT to reach out to for proactive engagement\. 
**Note**  
If you provide more than one contact, in the **Notes**, indicate the circumstances under which each contact should be used\. Include primary and secondary contact designations, and provide the hours of availability and time zones for each contact\. 

1. Choose **Save**\.

   The **Overview** page reflects the updated contact information\.

1. Choose **Edit proactive engagement feature**, choose **Enable**, and then choose **Save**\.

   When you first enable proactive engagement, the request goes to manual review\. During this time, the proactive engagement status indicates that your request is pending review\. The SRT will contact you to schedule an architecture review, which includes a review of your Route 53 health check configurations\. When the review is complete, the SRT completes your request to enable proactive engagement\. 

You can change SRT access and permissions at any time in the **Overview** page\.

Continue to [Step 6: Create a DDoS Dashboard in CloudWatch and Set CloudWatch Alarms ](deploy-waf-dashboard.md)\.