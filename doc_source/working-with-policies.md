# Working with AWS Firewall Manager Policies<a name="working-with-policies"></a>

AWS Firewall Manager provides the following types of policies: 
+ **AWS WAF** **policy** – This policy contains a AWS WAF Classic rule group and defines which resources will be protected by that rule group\. 
**Note**  
The latest version of AWS WAF was released in November, 2019\. AWS Firewall Manager currently works with the prior version, AWS WAF Classic, and not AWS WAF\. For information about AWS WAF Classic, see [AWS WAF Classic](classic-waf-chapter.md) 
+ **Shield Advanced policy** – This policy applies AWS Shield Advanced protection to specified accounts and resources\.
+ **Amazon VPC security group policy** – This type of policy gives you control over security groups that are in use throughout your organization in AWS Organizations and lets you enforce a baseline set of rules across your organization\. 

 A Firewall Manager policy is specific to the individual policy type\. If you want to enforce multiple policy types across accounts, you can create multiple policies\. You can create more than one policy for each type\. 

**Note**  
A rule group is a set of rules, and each rule includes conditions that you specify\. You can apply only one rule group to a policy, but you can apply the same rule group to multiple policies\.

If you add a new account to an organization that you created with AWS Organizations, Firewall Manager automatically applies the policy to the resources in that account that are within scope of the policy\. 