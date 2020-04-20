# Working with AWS Firewall Manager policies<a name="working-with-policies"></a>

AWS Firewall Manager provides the following types of policies: 
+ **AWS WAF** **policy** – Firewall Manager supports AWS WAF and AWS WAF Classic policies\. For both versions, you define which resources are protected by the policy\.
  + For the AWS WAF policy, you can define a set of rule groups to run first in the web ACL and a set of rule groups to run last\. In the accounts where you apply the web ACL, the account owner can add rules and rule groups to run in between the two Firewall Manager rule group sets\. 
  + For AWS WAF Classic, you create a policy that defines a single rule group\.
+ **Shield Advanced policy** – This policy applies AWS Shield Advanced protection to specified accounts and resources\. 
+ **Amazon VPC security group policy** – This type of policy gives you control over security groups that are in use throughout your organization in AWS Organizations and lets you enforce a baseline set of rules across your organization\. 

 A Firewall Manager policy is specific to the individual policy type\. If you want to enforce multiple policy types across accounts, you can create multiple policies\. You can create more than one policy for each type\. 

If you add a new account to an organization that you created with AWS Organizations, Firewall Manager automatically applies the policy to the resources in that account that are within scope of the policy\. 