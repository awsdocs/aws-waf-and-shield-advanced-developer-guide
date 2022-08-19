# Working with AWS Firewall Manager policies<a name="working-with-policies"></a>

AWS Firewall Manager provides the following types of policies: 

## <a name="w271aac13c26b5"></a>
+ **AWS WAF** **policy** – Firewall Manager supports AWS WAF and AWS WAF Classic policies\. For both versions, you define which resources are protected by the policy\.
  + For the AWS WAF policy, you can define a set of rule groups to run first in the web ACL and a set of rule groups to run last\. In the accounts where you apply the web ACL, the account owner can add rules and rule groups to run in between the two Firewall Manager rule group sets\. 
  + For AWS WAF Classic, you create a policy that defines a single rule group\.
+ **Shield Advanced policy** – This policy applies AWS Shield Advanced protection to specified accounts and resources\. 
+ **Amazon VPC security group policy** – This type of policy gives you control over security groups that are in use throughout your organization in AWS Organizations and lets you enforce a baseline set of rules across your organization\. 
+ **Network Firewall policy** – This policy applies AWS Network Firewall protection to your organization's VPCs\. 
+ **Amazon Route 53 Resolver DNS Firewall policy** – This policy applies DNS Firewall protections to your organization's VPCs\. 
+ **Cloud NGFW policy** – This policy applies Palo Alto Networks Cloud Next\-Generation Firewall \(Cloud NGFW\) protections and Cloud NGFW rulestacks to your organization's VPCs\.

A Firewall Manager policy is specific to the individual policy type\. If you want to enforce multiple policy types across accounts, you can create multiple policies\. You can create more than one policy for each type\. 

If you add a new account to an organization that you created with AWS Organizations, Firewall Manager automatically applies the policy to the resources in that account that are within scope of the policy\. 

## General settings for AWS Firewall Manager policies<a name="policies-general-settings"></a>

AWS Firewall Manager managed policies have some common settings and behaviors\. For all, you specify a name and define the scope of the policy, and you can use resource tagging to control policy scope\. You can choose to view the accounts and resources that are out of compliance without taking corrective action or to automatically remediate noncompliant resources\. 

For information about policy scope, see [AWS Firewall Manager policy scope](policy-scope.md)\. 