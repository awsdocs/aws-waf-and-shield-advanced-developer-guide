# Configure AWS SRT support<a name="authorize-srt"></a>

The Shield Response Team \(SRT\) are security engineers who specialize in DDoS event response\. You can optionally add permissions that allow the SRT to manage resources on your behalf during a DDoS event\. In addition, you can configure the SRT to proactively engage with you if the Route 53 health checks associated with your protected resources are unhealthy during a detected event\. Both of these additions to your protections enable quicker responses to DDoS events\. 

**Note**  
To use the services of the Shield Response Team \(SRT\), you must be subscribed to the [Business Support plan](https://aws.amazon.com/premiumsupport/business-support/) or the [Enterprise Support plan](https://aws.amazon.com/premiumsupport/enterprise-support/)\. 

The SRT can monitor AWS WAF request data and logs during application layer events to identify anomalous traffic\. They can help craft custom AWS WAF rules to mitigate offending traffic sources\. As needed, the SRT might make architectural recommendations to help you better align your resources with AWS recommendations\. 

For more information about the SRT, see [Shield Response Team \(SRT\) support](ddos-srt-support.md)\.

**To grant permissions to the SRT**

1. In the AWS Shield console **Overview** page, under **Configure AWS SRT support**, choose **Edit SRT access**\. The **Edit AWS Shield Response Team \(SRT\) access** page opens\.

1. For **SRT access setting** select one of the options: 
   + **Do not grant the SRT access to my account** – Shield removes any permissions you previously gave to the SRT to access your account and resources\.
   + **Create a new role for the SRT to access my account** – Shield creates a role that trusts the service principal `drt.shield.amazonaws.com`, which represents the SRT, and attaches the managed policy `AWSShieldDRTAccessPolicy` to it\. The managed policy allows the SRT to make AWS Shield Advanced and AWS WAF API calls on your behalf and to access your AWS WAF logs\. For more information about the managed policy, see [AWS managed policy: AWSShieldDRTAccessPolicy](shd-security-iam-awsmanpol.md#shd-security-iam-awsmanpol-AWSShieldDRTAccessPolicy)\.
   + **Choose an existing role for the SRT to access my accounts** – For this option, you must modify the configuration of the role in AWS Identity and Access Management \(IAM\) as follows: 
     + Attach the managed policy `AWSShieldDRTAccessPolicy` to the role\. This managed policy allows the SRT to make AWS Shield Advanced and AWS WAF API calls on your behalf and to access your AWS WAF logs\. For more information about the managed policy, see [AWS managed policy: AWSShieldDRTAccessPolicy](shd-security-iam-awsmanpol.md#shd-security-iam-awsmanpol-AWSShieldDRTAccessPolicy)\. For information about attaching the managed policy to your role, see [Attaching and Detaching IAM Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_manage-attach-detach.html)\. 
     + Modify the role to trust the service principal `drt.shield.amazonaws.com`\. This is the service principal that represents the SRT\. For more information, see [IAM JSON Policy Elements: Principal](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_principal.html)\. 

1. Choose **Save** to save your changes\. 

For more information about giving the SRT access to your protections and data, see [Configuring access for the Shield Response Team \(SRT\)](ddos-srt-access.md)\. 

**To enable SRT proactive engagement**

1. In the AWS Shield console **Overview** page, under **Proactive engagement and contacts**, in the contacts area, choose **Edit**\.

   In the **Edit contacts** page, provide the contact information for the people that you want the SRT to contact for proactive engagement\. 

   If you provide more than one contact, in the **Notes**, indicate the circumstances under which each contact should be used\. Include primary and secondary contact designations, and provide the hours of availability and time zones for each contact\. 

   Example contact notes: 
   + This is a hotline that's staffed 24x7x365\. Please work with the responding analyst and they will get the appropriate person on the call\. 
   + Please contact me if the hotline doesn't respond within 5 minutes\.

1. Choose **Save**\. 

   The **Overview** page reflects the updated contact information\.

1. Choose **Edit proactive engagement feature**, choose **Enable**, and then choose **Save** to enable proactive engagement\. 

For more information about proactive engagement, see [Configuring proactive engagement](ddos-srt-proactive-engagement.md)\.