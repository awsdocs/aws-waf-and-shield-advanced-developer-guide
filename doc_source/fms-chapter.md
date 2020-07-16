# AWS Firewall Manager<a name="fms-chapter"></a>

AWS Firewall Manager simplifies your AWS WAF, AWS Shield Advanced, and Amazon VPC security groups administration and maintenance tasks across multiple accounts and resources\. With Firewall Manager, you set up your AWS WAF firewall rules, Shield Advanced protections, and Amazon VPC security groups just once\. The service automatically applies the rules and protections across your accounts and resources, even as you add new resources\. 

Firewall Manager provides these benefits:
+ Helps to protect resources across accounts
+ Helps to protect all resources of a particular type, such as all Amazon CloudFront distributions
+ Helps to protect all resources with specific tags
+ Automatically adds protection to resources that are added to your account
+ Allows you to subscribe all member accounts in an AWS Organizations organization to AWS Shield Advanced, and automatically subscribes new in\-scope accounts that join the organization
+ Allows you to apply security group rules to all member accounts or specific subsets of accounts in an AWS Organizations organization, and automatically applies the rules to new in\-scope accounts that join the organization
+ Lets you use your own rules, or purchase managed rules from AWS Marketplace

Firewall Manager is particularly useful when you want to protect your entire organization rather than a small number of specific accounts and resources, or if you frequently add new resources that you want to protect\. Firewall Manager also provides centralized monitoring of DDoS attacks across your organization\.

**Topics**
+ [AWS Firewall Manager pricing](aws-fms-pricing.md)
+ [AWS Firewall Manager prerequisites](fms-prereq.md)
+ [Getting started with AWS Firewall Manager AWS WAF policies](getting-started-fms.md)
+ [Getting started with AWS Firewall Manager AWS Shield Advanced policies](getting-started-fms-shield.md)
+ [Getting started with AWS Firewall Manager Amazon VPC security group policies](getting-started-fms-security-group.md)
+ [Working with AWS Firewall Manager policies](working-with-policies.md)
+ [Viewing resource compliance for a policy](fms-compliance.md)
+ [AWS Firewall Manager findings](fms-findings.md)
+ [Designating a different account as the AWS Firewall Manager administrator account](fms-change-administrator.md)
+ [Security in AWS Firewall Manager](fms-security.md)
+ [AWS Firewall Manager quotas](fms-limits.md)