# Designating a different account as the AWS Firewall Manager administrator account<a name="fms-change-administrator"></a>

To use AWS Firewall Manager, you must log in to the console with a Firewall Manager administrator account\. You can designate only one account in an organization as a Firewall Manager administrator account\. It can be an AWS Organizations master account or a member account\. To set up an administrator account for the first time, see [Step 2: Set the AWS Firewall Manager administrator account](enable-integration.md)\. 

If you designate an account as an administrator account, and you later want to designate a different account as the administrator account, perform the following procedure\. 

**Important**  
To designate a different account, you first must revoke administrator privileges from the current administrator account\. When you revoke the privileges, all Firewall Manager policies created by that account are deleted\. You then must sign into Firewall Manager with the AWS Organizations master account to designate a new administrator account\. <a name="fms-change-administrator-procedure"></a>

**To designate a different account as the AWS Firewall Manager administrator account \(console\)**

1. Sign in to the AWS Management Console using the current Firewall Manager administrator account, and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 

1. In the navigation pane, choose **Settings**\.

1. Choose **Revoke administrator account**\.
**Important**  
When you revoke administrator privileges from the current administrator account, all Firewall Manager policies created by that account are deleted\.

1. Sign out of the AWS Management console\.

1. Sign in to the AWS Management Console using your AWS Organizations master account\. You can sign in using your root user credentials for the account \(not recommended\) or you can sign in using an IAM user or IAM role within the account that has equivalent permissions\.

1. Open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 

1. Choose **Get started**\.

1. Type an account ID to associate with Firewall Manager\. This account will be the new Firewall Manager administrator account\. It can be the master account that you are signed in with or it can be a member account in your organization\. If the account ID that you type is a member account and not the master account, Firewall Manager sets the appropriate permissions for the member account\. 
**Note**  
The account is given permission to create and manage AWS WAF rules and rule groups and AWS WAF Classic rules across all accounts within the organization\.

1. Choose **Set administrator**\.

## Closing the AWS Firewall Manager administrator account<a name="closed-admin-account"></a>

If you close your AWS Firewall Manager Administrator account without first revoking that account \(as described in the preceding step\), then:
+ AWS revokes the account’s administrator access from Firewall Manager\. After AWS revokes the account’s administrator access from Firewall Manager, all Firewall Manager policies applied to any account previously governed by the administrator account will be deactivated and such policy protection will no longer be applied to any of these accounts\.
+ AWS retains the Firewall Manager policy data for the account for 90 days from the effective date of your Administrator account closure\. If you elect to reopen the previously closed account during this 90\-day window, AWS reassigns the account as the Firewall Manager administrator and recovers the account’s previous Firewall Manager policy data\.
+ After the 90\-day window expires, if the closed account has not been reopened, AWS permanently deletes all Firewall Manager policy data for that account\.