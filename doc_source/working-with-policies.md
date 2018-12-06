# Working with AWS Firewall Manager Policies<a name="working-with-policies"></a>

An AWS Firewall Manager policy contains the rule group that you want to apply to your resources\. A rule group is a set of rules, and each rule includes conditions that you specify\. You can apply only one rule group to a policy, but you can apply the same rule group to multiple policies\.

Firewall Manager applies the policy to resource types that you specify \(such as CloudFront distributions or Application Load Balancers\) belonging to specified accounts within your organization in AWS Organizations\.

If you add a new account to your organization, Firewall Manager automatically applies the policy to the specified resources in that account\. 

**Topics**
+ [Creating an AWS Firewall Manager Policy](create-policy.md)
+ [Deleting an AWS Firewall Manager Policy](policy-deleting.md)