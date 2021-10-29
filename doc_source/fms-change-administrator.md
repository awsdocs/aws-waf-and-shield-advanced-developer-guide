# Changing the AWS Firewall Manager administrator account<a name="fms-change-administrator"></a>

To use AWS Firewall Manager, you must log in to the console with a Firewall Manager administrator account\. You can designate only one account in an organization as a Firewall Manager administrator account\. 

To set up an administrator account for the first time, see [AWS Firewall Manager prerequisites](fms-prereq.md)\. 

After you designate an account as an administrator account, if you later want to designate a different account as the administrator account, perform the following procedure\. 

**Important**  
To designate a different account, you first must revoke administrator privileges from the current administrator account\. When you revoke the privileges, all Firewall Manager policies created by that account are deleted\. You then must sign into Firewall Manager with the AWS Organizations management account to designate a new administrator account\. <a name="fms-change-administrator-procedure"></a>

**To designate a different account as the AWS Firewall Manager administrator account \(console\)**

1. Sign in to the AWS Management Console using your Firewall Manager administrator account, and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fmsv2](https://console.aws.amazon.com/wafv2/fmsv2)\. 

1. In the navigation pane, choose **Settings**\.

1. Choose **Revoke administrator account**\.
**Important**  
When you revoke administrator privileges from the current administrator account, all Firewall Manager policies created by that account are deleted\.

1. Sign out of the AWS Management Console\.

1. Sign in to the AWS Management Console using your AWS Organizations management account\. You can sign in using your root user credentials for the account \(not recommended\) or you can sign in using an IAM user or IAM role within the account that has equivalent permissions\.

1. Open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fmsv2](https://console.aws.amazon.com/wafv2/fmsv2)\. 

1. Choose **Get started**\.

1. Type an account ID to associate with Firewall Manager\. This account will be the new Firewall Manager administrator account\. 

   Firewall Manager sets the appropriate permissions for the member account that you provide\. 
**Note**  
The account is given permission to create and manage AWS WAF rules and rule groups and AWS WAF Classic rules across all accounts within the organization\.

1. Choose **Set administrator**\.