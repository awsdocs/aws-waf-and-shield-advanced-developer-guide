# Step 1: Join and configure AWS Organizations<a name="join-aws-orgs"></a>

To use Firewall Manager, your account must be a member of the organization in the AWS Organizations service where you want to use your Firewall Manager policies\. 

**Note**  
For information about Organizations, see [AWS Organizations User Guide](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_introduction.html)\. 

**To establish the required AWS Organizations membership and configuration**

1. Choose an account to use as the Firewall Manager administrator for the organization in Organizations\. 

1. If your chosen account isn't already a member of the organization, have it join\. Follow the guidance at [Inviting an AWS account to join your organization](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_accounts_invites.html)\.

1. AWS Organizations has two available feature sets: *consolidated billing features* and *all features*\. To use Firewall Manager, your organization must be enabled for all features\. If your organization is configured only for consolidated billing, follow the guidance at [Enabling All Features in Your Organization](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_org_support-all-features.html)\.