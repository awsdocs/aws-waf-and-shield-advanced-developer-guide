# AWS Firewall Manager<a name="fms-chapter"></a>

AWS Firewall Manager simplifies your AWS WAF administration and maintenance tasks across multiple accounts and resources\. With Firewall Manager, you set up your firewall rules just once\. The service automatically applies your rules across your accounts and resources, even as you add new resources\. 

Firewall Manager provides these benefits:
+ Helps to protect resources across accounts
+ Helps to protect all resources of a particular type, such as all Amazon CloudFront distributions
+ Helps to protect all resources with specific tags
+ Automatically adds protection to resources that are added to your account
+ Lets you use your own custom rules, or purchase managed rules from AWS Marketplace

Firewall Manager is particularly useful when you have a large number of resources that you want to protect with AWS WAF, or if you frequently add new resources that you want to protect\.

To use Firewall Manager, you add rules to a rule group, and you add the rule group to a policy\. Firewall Manager applies the policy to resource types that you specify \(such as CloudFront distributions or Application Load Balancers\) in all accounts within your organization in AWS Organizations\. If you add a new account to your organization, Firewall Manager automatically applies the policy to the specified resources in that account\.

**Topics**
+ [AWS Firewall Manager Pricing](aws-fms-pricing.md)
+ [AWS Firewall Manager Prerequisites](fms-prereq.md)
+ [Getting Started with AWS Firewall Manager](getting-started-fms.md)
+ [AWS Firewall Manager Limits](fms-limits.md)
+ [Working with Rule Groups](working-with-rule-groups.md)
+ [Working with AWS Firewall Manager Policies](working-with-policies.md)
+ [Viewing Resource Compliance with a Policy](fms-compliance.md)
+ [Designating a Different Account as the AWS Firewall Manager Administrator Account](fms-change-administrator.md)