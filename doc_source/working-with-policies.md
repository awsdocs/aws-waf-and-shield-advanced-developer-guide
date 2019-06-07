# Working with AWS Firewall Manager Policies<a name="working-with-policies"></a>

AWS Firewall Manager provides two types of policies: 
+ **Shield Advanced policy** – This policy applies AWS Shield Advanced protection to specified accounts and resources\.
+ **AWS WAF** **policy** – This policy contains a rule group and defines which resources will be protected by that rule group\. 

 A Firewall Manager policy is specific to either AWS WAF or Shield Advanced\. If you want to enforce both AWS WAF rules and Shield Advanced protection across accounts, you can create multiple policies\. You can create one or more policies for AWS WAF rules, and one or more policies for Shield Advanced\.

**Note**  
A rule group is a set of rules, and each rule includes conditions that you specify\. You can apply only one rule group to a policy, but you can apply the same rule group to multiple policies\.

If you add a new account to an organization that you created with AWS Organizations, Firewall Manager automatically applies the policy to the specified resources in that account\. 

**Note**  
When using Firewall Manager to protect Amazon API Gateway resources, Firewall Manager will typically apply the appropriate Firewall Manager policy to new in\-scope API Gateway stages within seconds\. However if you create a new stage as part of creating a new deployment using the API Gateway console or the `createDeployment` API, it might take up to 24 hours until Firewall Manager applies the policy\.

**Topics**
+ [Creating an AWS Firewall Manager Policy](create-policy.md)
+ [Deleting an AWS Firewall Manager Policy](policy-deleting.md)
+ [AWS Shield Advanced Policy Scope Changes](policy-scope-changes.md)