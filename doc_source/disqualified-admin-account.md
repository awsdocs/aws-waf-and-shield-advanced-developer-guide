# Disqualifying changes to the AWS Firewall Manager administrator account<a name="disqualified-admin-account"></a>

Some changes to the AWS Firewall Manager administrator account can disqualify it from remaining the administrator account\. 

This section describes the changes that can disqualify the Firewall Manager administrator account, and how AWS and Firewall Manager handle these changes\. 

## Account removed from the organization in AWS Organizations<a name="admin-account-not-in-org"></a>

If the AWS Firewall Manager administrator account is removed from the organization in AWS Organizations, it can no longer administer policies for the organization\. Firewall Manager takes one of the following actions: 
+ **Account with no policies** – If the Firewall Manager administrator account has no Firewall Manager policies, Firewall Manager revokes the administrator account\. 
+ **Account with Firewall Manager policies** – If the Firewall Manager administrator account has Firewall Manager policies, AWS retains the Firewall Manager policy data for the account for seven days from the effective date of the administrator account removed from the organization\. After seven days, Firewall Manager deactivates any policies that were managed by the administrator account\. The protections that were provided by those policies are stopped across the organization\.

## Account closed<a name="closed-admin-account"></a>

If you close the account that you're using for the AWS Firewall Manager administrator, AWS and Firewall Manager handle the closure as follows: 
+ AWS revokes the account’s administrator access from Firewall Manager and Firewall Manager deactivates any policies that were managed by the administrator account\. The protections that were provided by those policies are stopped across the organization\. 
+ AWS retains the Firewall Manager policy data for the account for 90 days from the effective date of the administrator account closure\. During this 90\-day period, you can reopen the closed account\. 
  + If you reopen the closed account during the 90\-day period, AWS reassigns the account as the Firewall Manager administrator and recovers the Firewall Manager policy data for the account\. 
  + Otherwise, at the end of the 90\-day period, AWS permanently deletes all Firewall Manager policy data for the account\.