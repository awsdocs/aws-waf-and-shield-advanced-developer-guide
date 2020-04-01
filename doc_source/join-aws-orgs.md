# Step 1: Join AWS Organizations<a name="join-aws-orgs"></a>

To use Firewall Manager, your account must be a member of an organization in the AWS Organizations service\. If your account is already a member, you can skip this step and go to [Step 2: Set the AWS Firewall Manager administrator account](enable-integration.md)\.

**Note**  
AWS Organizations has two available feature sets: *consolidated billing features* and *all features*\. To use Firewall Manager, the organization that you belong to must be enabled for [all features](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_getting-started_concepts.html#feature-set)\. If your organization is configured only for consolidated billing, see [Enabling All Features in Your Organization](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_org_support-all-features.html)\.

If your account is not part of an organization, create or join an organization as described in [Creating and Managing an AWS Organizations](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_org.html)\.

After your account is a member of an organization, go to [Step 2: Set the AWS Firewall Manager administrator account](enable-integration.md)\.