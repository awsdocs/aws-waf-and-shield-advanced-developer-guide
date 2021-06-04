# Step 2: Set the AWS Firewall Manager administrator account<a name="enable-integration"></a>

This procedure uses the account and organization that you chose and configured in the preceding step\.

When you set the Firewall Manager administrator account, Firewall Manager automatically sets it as the AWS Organizations Delegated Administrator for Firewall Manager\. This allows Firewall Manager to access information about the organizational units \(OUs\)\. You can use OUs to specify the scope of your Firewall Manager policies\. For more information about setting policy scope, see the guidance for the individual policy types under [Creating an AWS Firewall Manager policy](create-policy.md)\. For more information about Organizations and management accounts, see [Managing the AWS Accounts in Your Organization](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_accounts.html)\.<a name="enable-integration-procedure-console"></a>

**To set the Firewall Manager administrator account**

1. Sign in to the AWS Management Console using an existing AWS Organizations management account\. You can sign in using the account's root user \(not recommended\) or another IAM user or IAM role within the account that has equivalent permissions\.

1. Open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fmsv2](https://console.aws.amazon.com/wafv2/fmsv2) \. 

1. Choose **Get started**\.

1. Type the ID of the account that you've chosen to use as the Firewall Manager administrator\. 
**Note**  
The account that you enter in this step is given permission to create and manage Firewall Manager policies across all accounts within your organization\.

1. Choose **Set administrator**\.

For more information about managing the Firewall Manager administrator account, see [Managing the AWS Firewall Manager administrator](fms-administrator.md)\.