# Step 3: \(Optional\) Authorize the DDoS Response Team<a name="authorize-DRT"></a>

One of the benefits of AWS Shield Advanced is support from the DDoS response team \(DRT\)\. When you experience a potential DDoS attack, you can contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\. If necessary, the Support Center escalates your issue to the DRT\. The DRT can help you analyze the suspicious activity and assist you in mitigating the issue\. This mitigation often involves creating or updating AWS WAF rules and web access control lists \(web ACLs\) in your account\. The DRT can inspect your AWS WAF configuration and create or update AWS WAF rules and web ACLs for you, but the team needs your authorization to do so\. We recommend that as part of setting up AWS Shield Advanced, you proactively provide the DRT with the needed authorization\. Providing authorization ahead of time helps prevent mitigation delays in the event of an actual attack\. 

If you do *not* want to authorize the DRT to mitigate potential attacks on your behalf, choose **Do not grant the DRT access to my account** and then **Finish**\. Otherwise, continue with the following steps\.

**Note**  
To use the services of the DRT, you must be subscribed to the [Business Support plan](https://aws.amazon.com/premiumsupport/business-support/) or the [Enterprise Support plan](https://aws.amazon.com/premiumsupport/enterprise-support/)\.<a name="authorize-DRT-procedure"></a>

**To authorize the DRT to mitigate potential attacks on your behalf**

1. After you complete [Step 1: Activate AWS Shield Advanced](enable-ddos-prem.md), the **Authorize DRT support** page appears\. Select either **Create new role for the DRT to access my account** or **Choose an existing role for the DRT to access my account**\.

   If you choose to use an existing role, must you must attach the `AWSShieldDRTAccessPolicy` managed policy to the role\. For more information, see [Attaching and Detaching IAM Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_manage-attach-detach.html)\. If you choose **Create new role for the DRT to access my account**, this policy will be attached to the role automatically\.

   If you choose to use an existing role, the role must also trust the service principal ` drt.shield.amazonaws.com`\. For more information, see [IAM JSON Policy Elements: Principal](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_principal.html)\. 

   The `AWSShieldDRTAccessPolicy` managed policy gives the DRT full access to only your AWS WAF and Shield resources\. The policy enables the DRT to inspect your AWS WAF configuration and create or update AWS WAF rules and web ACLs on your behalf\. The DRT takes these actions only if explicitly authorized by you\.

1. Complete the necessary information, either the new role name or the existing role name\.

1. \(Optional\) Choose **Authorize the DRT to access your flow logs stored in Amazon S3 buckets**, and then type the name of your Amazon S3 bucket where those logs are stored\. Choose **Add bucket**\. Repeat as necessary, adding more buckets, to a maximum of 10\. 

1. We send notifications of possible DDoS activity to the email address that is associated with your account\. If you want us to send notifications to additional email addresses, type each address in the box and choose **Add email address**\. Repeat as necessary to add more email addresses, to a maximum of 10\.

1. Choose **Finish**\. 

You can change DRT access and permissions at any time by following the instructions in [Editing AWS Shield Advanced Settings](ddos-edit-drt.md)\.

After you authorize the DRT to act on your behalf, we recommend that you follow the instructions in [Step 4: Create a DDoS Dashboard in CloudWatch and Set CloudWatch Alarms ](deploy-waf-dashboard.md)\.