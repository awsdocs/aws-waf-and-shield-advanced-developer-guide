# Resource sharing for Network Firewall and DNS Firewall policies<a name="resource-sharing"></a>

To manage Firewall Manager Network Firewall and DNS Firewall policies, you must enable resource sharing with AWS Organizations in AWS Resource Access Manager\. This allows Firewall Manager to deploy protections across your accounts when you create these policy types\.

To enable resource sharing, follow the instructions at [Enable Sharing with AWS Organizations](https://docs.aws.amazon.com/ram/latest/userguide/getting-started-sharing.html#getting-started-sharing-orgs) in the *AWS Resource Access Manager User Guide*\. 

**Problems with resource sharing**  
You might encounter problems with resource sharing, either when you use AWS RAM to enable it, or when you're working on Firewall Manager policies that require it\. 

Examples of these problems include the following: 
+ When you follow the instructions to enable sharing, in the AWS RAM console, the choice **Enable sharing with AWS Organizations** is grayed out and not available for selection\.
+ When you work in Firewall Manager on a policy that requires resource sharing, the policy is marked as non\-compliant and you see messages indicating that resource sharing or AWS RAM isn't enabled\. 

If you encounter problems with resource sharing, use the following procedure to try to enable it\. 

**Try again to enable resource sharing**
+ Try again to enable sharing using one of the following options: 
  + \(Option\) Through the AWS RAM console, follow the instructions at [Enable Sharing with AWS Organizations](https://docs.aws.amazon.com/ram/latest/userguide/getting-started-sharing.html#getting-started-sharing-orgs) in the *AWS Resource Access Manager User Guide*\.
  + \(Option\) Using the AWS RAM API, call `EnableSharingWithAwsOrganization`\. See the documentation at [EnableSharingWithAwsOrganization](https://docs.aws.amazon.com/ram/latest/APIReference/API_EnableSharingWithAwsOrganization.html)\.