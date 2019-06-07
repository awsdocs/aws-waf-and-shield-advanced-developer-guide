# AWS Firewall Manager<a name="fms-chapter"></a>

AWS Firewall Manager simplifies your AWS WAF and AWS Shield Advanced administration and maintenance tasks across multiple accounts and resources\. With Firewall Manager, you set up your AWS WAF firewall rules and Shield Advanced protections just once\. The service automatically applies the rules and protections across your accounts and resources, even as you add new resources\. 

Firewall Manager provides these benefits:
+ Helps to protect resources across accounts
+ Helps to protect all resources of a particular type, such as all Amazon CloudFront distributions
+ Helps to protect all resources with specific tags
+ Automatically adds protection to resources that are added to your account
+ Allows you to subscribe all member accounts in an AWS Organizations organization to AWS Shield Advanced, and automatically subscribes new in\-scope accounts that join the organization
+ Lets you use your own custom rules, or purchase managed rules from AWS Marketplace

Firewall Manager is particularly useful when you want to protect your entire organization rather than a limited number of specific accounts and resources, or if you frequently add new resources that you want to protect\. Firewall Manager also provides centralized monitoring of DDoS attacks across your organization\.

**Topics**
+ [AWS Firewall Manager Pricing](aws-fms-pricing.md)
+ [AWS Firewall Manager Prerequisites](fms-prereq.md)
+ [Getting Started with AWS Firewall Manager to Enable AWS WAF Rules](getting-started-fms.md)
+ [Getting Started with AWS Firewall Manager to Enable AWS Shield Advanced Protection](getting-started-fms-shield.md)
+ [AWS Firewall Manager Limits](fms-limits.md)
+ [Working with Rule Groups](working-with-rule-groups.md)
+ [Working with AWS Firewall Manager Policies](working-with-policies.md)
+ [Tutorial: Creating a Policy with Hierarchical Rules](hierarchical-rules.md)
+ [Viewing Resource Compliance with a Policy](fms-compliance.md)
+ [Designating a Different Account as the AWS Firewall Manager Administrator Account](fms-change-administrator.md)