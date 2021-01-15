# Working with AWS Firewall Manager policies<a name="working-with-policies"></a>

AWS Firewall Manager provides the following types of policies: 
+ **AWS WAF** **policy** – Firewall Manager supports AWS WAF and AWS WAF Classic policies\. For both versions, you define which resources are protected by the policy\.
  + For the AWS WAF policy, you can define a set of rule groups to run first in the web ACL and a set of rule groups to run last\. In the accounts where you apply the web ACL, the account owner can add rules and rule groups to run in between the two Firewall Manager rule group sets\. 
  + For AWS WAF Classic, you create a policy that defines a single rule group\.
+ **Shield Advanced policy** – This policy applies AWS Shield Advanced protection to specified accounts and resources\. 
+ **Amazon VPC security group policy** – This type of policy gives you control over security groups that are in use throughout your organization in AWS Organizations and lets you enforce a baseline set of rules across your organization\. 
+ **Network Firewall policy** – This policy applies AWS Network Firewall protection to your organization's VPCs\. 

A Firewall Manager policy is specific to the individual policy type\. If you want to enforce multiple policy types across accounts, you can create multiple policies\. You can create more than one policy for each type\. 

If you add a new account to an organization that you created with AWS Organizations, Firewall Manager automatically applies the policy to the resources in that account that are within scope of the policy\. 

## General settings for AWS Firewall Manager policies<a name="policies-general-settings"></a>

AWS Firewall Manager managed policies have some common settings and behaviors\. For all, you specify a name and define the scope of the policy, and you can use resource tagging to control policy scope\. You can choose to view the accounts and resources that are out of compliance without taking corrective action or to automatically remediate noncompliant resources\. 

Policy scope defines where to apply the policy\. You can apply centrally controlled security group policies to all of your resources and to all of your accounts in your organization in AWS Organizations or to a select subset of your accounts and resources\. Once in place, Firewall Manager manages your policies continuously, and applies them to new AWS accounts and resources as they are added, according to the policy scope\. 

**AWS accounts in scope**  
The settings that you provide to define the AWS accounts affected by the policy determine which of the accounts in your AWS organization to apply the policy to\. You can choose to apply the policy in one of the following ways: 
+ To all accounts in your organization
+ To only a specific list of included account numbers and AWS Organizations organizational units \(OUs\)
+ To all except a specific list of excluded account numbers and AWS Organizations organizational units \(OUs\)

For information about AWS Organizations, see [AWS Organizations User Guide](https://docs.aws.amazon.com/organizations/latest/userguide/)\. 

Whichever option you choose, when you add a new account to your organization, Firewall Manager automatically assesses it against these settings in each policy and applies the policy as indicated\. For example, if you choose to apply the policy to all accounts except the account numbers in the list, when you add a new account, Firewall Manager applies the policy if the new account number isn't in the exclude list\. 

**Resources in scope**  
The settings that you provide for resources determine which resources in the in\-scope accounts and resource types to apply the policy to\. You can choose one of the following: 
+ All resources 
+ All resources except those that have all the tags that you specify
+ Resources that have all the tags that you specify

For more information about tagging your resources, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\. 

Whichever option you choose, when you add a new resource to your organization, Firewall Manager automatically assesses the resources against these settings in each policy and applies the policy as indicated\. For example, if you choose to apply the policy only to resources that have all the tags in the list, when you add or update a resource within your policy's account and resource type parameters, Firewall Manager compares the resource's tags to the list and applies the policy if the resource has all the tags\. 