# Managing the AWS Firewall Manager administrator<a name="fms-administrator"></a>

You use your Firewall Manager administrator account to manage your Firewall Manager policies\. When you set the Firewall Manager administrator account, Firewall Manager automatically sets it as the AWS Organizations Delegated Administrator for Firewall Manager\. This allows Firewall Manager to access information about the organizational units \(OUs\) that you use to specify the scope of your Firewall Manager policies\. For more information about Organizations and management accounts, see [Managing the AWS Accounts in Your Organization](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_accounts.html)\.

To begin using Firewall Manager, you set up your Firewall Manager administrator account and perform other required steps\. To do this, follow the guidance under [AWS Firewall Manager prerequisites](fms-prereq.md)\. 

This topic provides information and guidance for managing your existing administrator account\. 

**Required settings for the Firewall Manager administrator**  
The Firewall Manager administrator account must have the following settings: 
+ It must be a member of the organization in AWS Organizations where you want to apply your Firewall Manager policies\. 
+ It cannot be the organization's management account\.
+ It must be designated as the Firewall Manager administrator by the Organizations management account for the organization\.