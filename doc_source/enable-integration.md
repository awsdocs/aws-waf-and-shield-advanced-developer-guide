# Step 2: Set the AWS Firewall Manager administrator account<a name="enable-integration"></a>

AWS Firewall Manager must be associated with the management account of your AWS organization or associated with a member account that has permissions equivalent to those of the management account\. The account that you associate with Firewall Manager is called the Firewall Manager administrator account\. For more information about AWS Organizations and management accounts, see [Managing the AWS Accounts in Your Organization](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_accounts.html)\.<a name="enable-integration-procedure-console"></a>

**To set the Firewall Manager administrator account \(console\)**

1. Sign in to the AWS Management Console using an existing AWS Organizations management account\. You can sign in using the account's root user \(not recommended\) or another IAM user or IAM role within the account that has equivalent permissions\.

1. Open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fmsv2](https://console.aws.amazon.com/wafv2/fmsv2) \. 

1. Choose **Get started**\.

1. Type the account ID for the account that you want to use as the Firewall Manager administrator\. The account ID can be for the account that you are signed in with, or a different account\. If the account ID that you type is not an AWS Organizations management account, Firewall Manager sets the appropriate permissions for the member account that you specify\.
**Note**  
The account that you enter in this step is given permission to create and manage AWS WAF rules across all accounts within your organization\.

1. Choose **Set administrator**\.

For more information about managing the Firewall Manager administrator account, see [Managing the AWS Firewall Manager administrator](fms-administrator.md)\.

After you set the Firewall Manager administrator account, go to [Step 3: Enable AWS Config](enable-config.md)\.