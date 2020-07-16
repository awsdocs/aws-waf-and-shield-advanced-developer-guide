# Step 4: \(Optional\) Prepare for response team engagement<a name="authorize-DRT"></a>

With AWS Shield Advanced, you can engage with the AWS DDoS Response Team \(DRT\) if your application is unhealthy as the result of a possible DDoS attack\. 

**Note**  
To contact the DRT, you must be subscribed to the [Business Support plan](https://aws.amazon.com/premiumsupport/business-support/) or the [Enterprise Support plan](https://aws.amazon.com/premiumsupport/enterprise-support/)\. If you aren't subscribed to either plan, some of the options described in this section might not be visible in your account or accessible via the AWS Shield Advanced API\.

You can contact the DRT in one of the following ways: 
+ **Support case** – You can open a case under **AWS Shield** in the [AWS Support Center](https://docs.aws.amazon.com/awssupport/latest/user/case-management.html)\. If your application is unhealthy, open a case using the highest severity available for your support plan and select either the **Phone** or **Chat** contact options\. In the description for your case, provide as much detail as possible\. Be sure to provide information about any protected resources that might be affected, and the current state of your end user experience\. For example, if your user experience is degraded or parts of your application are currently unavailable, provide that information\. 
+ **Proactive engagement** – With AWS Shield Advanced proactive engagement, the DRT contacts you directly if the Amazon Route 53 health check associated with your protected resource becomes unhealthy during an event that's detected by Shield Advanced\. For more information about this option, see [Shield Advanced proactive engagement](ddos-overview.md#ddos-advanced-proactive-engagement)\.

**Grant the DRT limited access to certain APIs and S3 buckets that you designate**

AWS Shield Advanced automatically mitigates DDoS attacks against your resources\. Shield Advanced detects web application layer vectors, like web request floods and low\-and\-slow bad bots, but doesn't automatically mitigate them\. To mitigate web application layer vectors, you must employ AWS WAF rules or the DRT must employ the rules on your behalf\. 

**Note**  
Shield Advanced detects web application layer events when you protect Amazon CloudFront distributions and Application Load Balancers\. These events indicate a statistically significant deviation in traffic, compared to your application’s historical baseline\. You can choose to take no action if a deviation is expected or hasn't affected the health of your resource\.

The DRT can assist you with web application layer events if you grant limited access to your Shield Advanced and AWS WAF APIs, and access to the Amazon S3 bucket that contains your AWS WAF logs\. You can revoke access at any time\. The DRT engineers only access your APIs and AWS WAF logs with your authorization, limited to the scope of your support engagement\. <a name="authorize-DRT-procedure"></a>

**To give DRT authorization to assist with web application layer events on your behalf**

1. In the AWS WAF console, enable AWS WAF logging for each web ACL that's attached to a Shield Advanced protected resource\. For more information about AWS WAF logging, see [Logging Web ACL traffic information](logging.md)\. 

   For the DRT to view or process your AWS WAF logs, the logs must be in Amazon S3 buckets that satisfy the following requirements: 
   + The buckets must be in the same AWS account as the web ACL\. 
   + The buckets can be either plain text or SSE\-S3 encrypted\. For more information about Amazon S3 SSE\-S3 encryption, see [Protecting Data Using Server\-Side Encryption with Amazon S3\-Managed Encryption Keys \(SSE\-S3\)](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html) in the [Amazon Simple Storage Service Amazon Simple Storage Service Developer Guide](https://docs.aws.amazon.com/AmazonS3/latest/dev/Welcome.html)\.

     The DRT can't view or process logs that are stored in buckets that are encrypted with keys stored in AWS Key Management Service \(AWS KMS\)\. 
   + You can give the DRT permission to access a maximum of 10 buckets\. 

1. In the AWS Shield console summary, under **Authorize DRT Support**, choose **Edit**\.

1. Select either **Create new role for the DRT to access my account** or **Choose an existing role for the DRT to access my account**, and then enter the role name\. The role allows the DRT to inspect your Shield Advanced and AWS WAF configuration and create or update rules and web ACLs on your behalf\. If you use a new role, the appropriate policy is attached to the role automatically and the role is configured properly\.

   If you use an existing role, you must alter the role in AWS Identity and Access Management \(IAM\) as follows: 

   1. Attach the managed policy `AWSShieldDRTAccessPolicy` to the role\. The `AWSShieldDRTAccessPolicy` managed policy gives the DRT access to your AWS Shield Advanced and AWS WAF resources\. For more information, see [Attaching and Detaching IAM Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_manage-attach-detach.html)\. 

   1. Modify the role to trust the service principal `drt.shield.amazonaws.com`\. This is the service principal that represents the DRT\. For more information, see [IAM JSON Policy Elements: Principal](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_principal.html)\. 

1. For each Amazon S3 bucket where your AWS WAF logs are stored, enter the name of the bucket and choose **Add Bucket**\. You can add up to 10 buckets\.

   This grants the DRT the following permissions on the bucket: `s3:GetBucketLocation`, `s3:GetObject`, and `s3:ListBucket`\.

1. Choose **Grant Access**\.

**To enable DRT proactive engagement**

Shield Advanced proactive engagement allows you to engage with the DRT more quickly when the availability of your application is affected as the result of a possible attack\. When you have proactive engagement enabled, the DRT contacts you when a Shield Advanced event correlates to an unhealthy R53 health check on one or more of your protected resources\.

1. In the Shield Advanced console, under **Contacts and proactive engagement**, for each contact, choose **Add contact**\. You can add up to 10 contacts\. These are the people the DRT reaches out to for proactive engagement\.

1. Provide the email address and phone number for each contact\. Add any special instructions in the contact notes\. 
**Note**  
If you provide more than one point of contact, indicate the circumstances under which each contact should be used\. 

1. Choose **Save**\.

1. Choose **Enable proactive engagement**\.

   When you first enable proactive engagement, the request goes to manual review\. While the request is pending review, the console displays **Proactive engagement requested and pending\.** The DRT will contact you to schedule an architecture review, which includes a review of your Route 53 health check configuration\. When the review is complete, the DRT completes your request to enable proactive engagement\. 

You can change DRT access and permissions at any time by following the instructions in [Editing AWS Shield Advanced settings](ddos-edit-drt.md)\.

Continue to [Step 5: Configure Amazon CloudWatch alarms](ddos-get-started-cloudwatch.md)\.