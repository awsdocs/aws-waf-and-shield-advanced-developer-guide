# Security group policies<a name="security-group-policies"></a>

You can use AWS Firewall Manager security group policies to manage Amazon Virtual Private Cloud security groups for your organization in AWS Organizations\. You can apply centrally controlled security group policies to your entire organization or to a select subset of your accounts and resources\. You can also monitor and manage the security group policies that are in use in your organization, with auditing and usage security group policies\.

Firewall Manager continuously maintains your policies and applies them to accounts and resources as they are added or updated across your organization\. For information about AWS Organizations, see [AWS Organizations User Guide](https://docs.aws.amazon.com/organizations/latest/userguide/)\. For information about Amazon Virtual Private Cloud security groups, see [Security Groups for Your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html) in the [Amazon VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/)\.

You can use Firewall Manager security group policies to do the following across your AWS organization: 
+ Apply common security groups to specified accounts and resources\. 
+ Audit security group rules, to locate and remediate noncompliant rules\. 
+ Audit usage of security groups, to clean up unused and redundant security groups\. 

This section covers how Firewall Manager security groups policies work and provides guidance for using them\. For procedures to create security group policies, see [Creating an AWS Firewall Manager policy](create-policy.md)\.  

## General settings for security group policies<a name="security-group-policies-general"></a>

Security group policies in AWS Firewall Manager are similar to other Firewall Manager managed policies\. You pick a name and define the scope of the policy\. You can use resource tagging to control policy scope\. You can choose to view the accounts and resources that are out of compliance without taking corrective action or to automatically remediate noncompliant resources\. Once in place, Firewall Manager runs your security group policies continuously, and applies them to new AWS accounts and resources as they are added, according to the policy scope\. 

**AWS accounts in scope**  
The settings that you provide for the AWS accounts affected by the policy determine which of the accounts in your AWS organization to apply the security group policy to\. You can choose to apply the policy in one of the following ways: 
+ To all accounts in your organization
+ To only a specific list of included account numbers and AWS Organizations organizational units \(OUs\)
+ To all except a specific list of excluded account numbers and AWS Organizations organizational units \(OUs\)

Whichever option you choose, when you add a new account to your organization, Firewall Manager automatically assesses it against these settings in each security group policy and applies the policy as indicated\. For example, if you choose to apply the policy to all accounts except the account numbers in the list, when you add a new account, Firewall Manager applies the policy if the new account number isn't in the exclude list\.

**Resources in scope**  
The settings that you provide for resources determine which resources in the in\-scope accounts and resource types to apply the policy to\. You can choose one of the following: 
+ All resources 
+ All resources except those that have all the tags that you specify
+ Resources that have all the tags that you specify

For more information about tagging your resources, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\. 

Whichever option you choose, when you add a new resource to your organization, Firewall Manager automatically assesses the resources against these settings in each security group policy and applies the policy as indicated\. For example, if you choose to apply the policy only to resources that have all the tags in the list, when you add or update a resource within your policy's account and resource type parameters, Firewall Manager compares the resource's tags to the list and applies the policy if the resource has all the tags\. 

## Common security group policies<a name="security-group-policies-common"></a>

With a common security group policy, Firewall Manager provides a centrally controlled association of security groups to accounts and resources across your organization\. You specify where and how to apply the policy in your organization\. 

For guidance on creating a common security group policy using the console, see [Creating a common security group policy](create-policy.md#creating-firewall-manager-policy-common-security-group)\.

**Shared VPCs**  
In the policy scope settings for a common security group policy, you can choose to include shared VPCs\. This choice includes VPCs that are owned by another account and shared with an in\-scope account\. VPCs that in\-scope accounts own are always included\. For information about shared VPCs, see [Working with shared VPCs](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-sharing.html) in the [Amazon VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/)\. 

The following caveats apply to including shared VPCs\. These are in addition to the general caveats for security group policies at [Security group policy limitations](#security-groups-limitations)\.
+ Firewall Manager replicates the primary security group into the VPCs for each in\-scope account\. For a shared VPC, Firewall Manager replicates the primary security group once for each in\-scope account that the VPC is shared with\. This can result in multiple replicas in a single shared VPC\. 
+ When you create a new shared VPC, you won’t see it represented in the Firewall Manager security group policy details until after you create at least one resource in the VPC that's within the scope of the policy\. 
+ When you disable shared VPCs in a policy that had shared VPCs enabled, in the shared VPCs, Firewall Manager deletes the replica security groups that aren’t associated with any resources\. Firewall Manager leaves the remaining replica security groups in place, but stops managing them\. Removal of these remaining security groups requires manual management in each shared VPC instance\.

**Primary security groups**  
For each common security group policy, you provide AWS Firewall Manager with one or more primary security groups:
+ Primary security groups must be created by the Firewall Manager administrator account and can reside in any Amazon VPC instance in the account\. 
+ You manage your primary security groups through Amazon Virtual Private Cloud \(Amazon VPC\) or Amazon Elastic Compute Cloud \(Amazon EC2\)\. For information, see [Working with Security Groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#WorkingWithSecurityGroups) in the [Amazon VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/)\. 
+ You can name one or more security groups as primaries for a Firewall Manager security group policy\. By default, the number of security groups allowed in a policy is one, but you can submit a request to increase it\. For information, see [AWS Firewall Manager quotas](fms-limits.md)\.

**Policy rules settings**  
You can choose one or both of the following change control behaviors for the security groups and resources of your common security group policy:
+ Identify and revert any changes made by local users to replica security groups\. 
+ Disassociate any other security groups from the AWS resources that are within the policy scope\. 

**Policy creation and management**  
When you create your common security group policy, Firewall Manager replicates the primary security groups to every Amazon VPC instance within the policy scope, and associates the replicated security groups to accounts and resources that are in scope of the policy\. When you modify a primary security group, Firewall Manager propagates the change to the replicas\.

When you delete a common security group policy, you can choose whether to clean up the resources created by the policy\. For Firewall Manager common security groups, these resources are the replica security groups\. Choose the cleanup option unless you want to manually manage each individual replica after the policy is deleted\. For most situations, choosing the cleanup option is the simplest approach\.

**How replicas are managed**  
The replica security groups in the Amazon VPC instances are managed like other Amazon VPC security groups\. For information, see [Security Groups for Your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html) in the [Amazon VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/)\. 

## Content audit security group policies<a name="security-group-policies-audit"></a>

Use AWS Firewall Manager content audit security group policies to check and manage the rules that are in use in your organization's security groups\. You can apply a content audit security group policy to the same resource types as common security group policies, and you can also apply them to security groups themselves\. Content audit security group policies apply to all customer\-created security groups in use in your AWS organization, according to the scope that you define in the policy\.

For guidance on creating a content audit security group policy using the console, see [Creating a content audit security group policy](create-policy.md#creating-firewall-manager-policy-audit-security-group)\.

**Policy scope resource type**  
For the resource type of a content audit security group policy, you can choose the same types that are available to the common security group policy\. You can also choose security groups as a resource type\. Security groups are considered in scope of the policy if they explicitly are in scope or if they're associated with resources that are in scope\.

**Policy rule options**  
You can use either managed policy rules or custom policy rules for each content audit policy, but not both\.
+ **Managed policy rules** – In a policy with managed rules, you can use application and protocol lists to specify what's allowed and what's denied by the policy\. You can use lists that are managed by Firewall Manager\. You can also create and use your own application and protocol lists\. For information about these types of lists and your management options for custom lists, see [Managed lists](working-with-managed-lists.md)\.
+ **Custom policy rules** – In a policy with custom policy rules, you specify an existing security group as the audit security group for your policy\. You can use the audit security group rules as a template that defines the rules that are allowed or denied by the policy\. 

**Audit security groups**  
You must create audit security groups using your Firewall Manager administrator account, before you can use them in your policy\. You can manage security groups through Amazon Virtual Private Cloud \(Amazon VPC\) or Amazon Elastic Compute Cloud \(Amazon EC2\)\. For information, see [Working with Security Groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#WorkingWithSecurityGroups) in the [Amazon VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/)\. 

A security group that you use for a content audit security group policy is used by Firewall Manager only as a comparison reference for the security groups that are in scope of the policy\. Firewall Manager doesn't associate it with any resources in your organization\. 

The way that you define the rules in the audit security group depends on your choices in the policy rules settings:
+ **Managed policy rules** – For managed policy rules settings, you use an audit security group to override other settings in the policy, to explicitly allow or deny rules that otherwise might have another compliancy outcome\. 
  + If you choose to always *allow* the rules that are defined in the audit security group, any rule that matches one that's defined in the audit security group is considered *compliant* with the policy, regardless of the other policy settings\.
  + If you choose to always *deny* the rules that are defined in the audit security group, any rule that matches one that's defined in the audit security group is considered *noncompliant* with the policy, regardless of the other policy settings\.
+ **Custom policy rules** – For custom policy rules settings, the audit security group provides the example of what is acceptable or not acceptable in the in\-scope security group rules: 
  + If you choose to *allow* the use of the rules, all in\-scope security groups must only have rules that are *within* the allowed range of the policy's audit security group rules\. *In this case, the policy's security group rules provide the example of what's acceptable to do\.*
  + If you choose to *deny* the use of the rules, all in\-scope security groups must only have rules that are *not within* the allowed range of the policy's audit security group rules\. *In this case, the policy's security group provides the example of what's not acceptable to do\.*

**Policy creation and management**  
When you create an audit security group policy, you must have automatic remediation disabled\. The recommended practice is to review the effects of policy creation before enabling automatic remediation\. After you review the expected effects, you can edit the policy and enable automatic remediation\. When automatic remediation is enabled, Firewall Manager updates or removes rules that are noncompliant in in\-scope security groups\.

**Security groups affected by an audit security group policy**  
All security groups in your organization that are customer\-created are eligible to be in scope of an audit security group policy\. 

Replica security groups are not customer\-created and so aren't eligible to be directly in scope of an audit security group policy\. However, they can be updated as a result of the policy's automatic remediation activities\. A common security group policy's primary security group is customer\-created and can be in scope of an audit security group policy\. If an audit security group policy makes changes to a primary security group, Firewall Manager automatically propagates those changes to the replicas\. 

## Usage audit security group policies<a name="security-group-policies-usage"></a>

Use AWS Firewall Manager usage audit security group policies to monitor your organization for unused and redundant security groups and optionally perform cleanup\. When you enable automatic remediation for this policy, Firewall Manager does the following:

1. Consolidates redundant security groups, if you've chosen that option\.

1. Removes unused security groups, if you've chosen that option\. 

For guidance on creating a usage audit security group policy using the console, see [Creating a usage audit security group policy](create-policy.md#creating-firewall-manager-policy-usage-security-group)\.

**How Firewall Manager remediates redundant security groups**  
For security groups to be considered redundant, they must have exactly the same rules set and be in the same Amazon VPC instance\. To remediate a redundant security group set, Firewall Manager selects one of the security groups in the set to keep, and then associates it to all resources that are associated with the other security groups in the set\. Firewall Manager then disassociates the other security groups from the resources they were associated with, which renders them unused\. 

**Note**  
If you have also chosen to remove unused security groups, Firewall Manager does that next\. This can result in the removal of the security groups that are in the redundant set\.

**How Firewall Manager remediates unused security groups**  
For security groups to be considered unused, they must remain unused by any resource for the minimum number of minutes specified in the policy rule\. By default, this number is zero\. You can give this a higher setting, in order to allow yourself time to associate new security groups with resources\. Firewall Manager remediates unused security groups by deleting them from your account, according to your rules settings\. 

**Default account specification**  
When you create a usage audit security group policy through the console, Firewall Manager automatically chooses **Exclude the specified accounts and include all others**\. The service then puts the Firewall Manager administrator account in the list to exclude\. This is the recommended approach, and allows you to manually manage the security groups that belong to the Firewall Manager administrator account\. 

## Best practices for security group policies<a name="security-groups-best-practice"></a>

 This section lists recommendations for managing security groups using AWS Firewall Manager\.

**Exclude the Firewall Manager administrator account**  
When you set the policy scope, exclude the Firewall Manager administrator account\. When you create a usage audit security group policy through the console, this is the default option\. 

**Start with automatic remediation disabled**  
For content or usage audit security group policies, start with automatic remediation disabled\. Review the policy details information to determine the effects that automatic remediation would have\. When you are satisfied that the changes are what you want, edit the policy to enable automatic remediation\.

**Avoid conflicts if you also use outside sources to manage security groups**  
If you use a tool or service other than Firewall Manager to manage security groups, take care to avoid conflicts between your settings in Firewall Manager and the settings in your outside source\. If you use automatic remediation and your settings conflict, you can create a cycle of conflicting remediation that consumes resources on both sides\. 

For example, say you configure another service to maintain a security group for a set of AWS resources, and you configure a Firewall Manager policy to maintain a different security group for some or all of the same of resources\. If you configure either side to disallow any other security group to be associated with the in\-scope resources, that side will remove the security group association that's maintained by the other side\. If both sides are configured in this way, you can end up with a cycle of conflicting disassociations and associations\. 

Additionally, say that you create a Firewall Manager audit policy to enforce a security group configuration that conflicts with the security group configuration from the other service\. Remediation applied by the Firewall Manager audit policy can update or delete that security group, putting it out of compliance for the other service\. If the other service is configured to monitor and automatically remediate any problems it finds, it will recreate or update the security group, putting it again out of compliance with the Firewall Manager audit policy\. If the Firewall Manager audit policy is configured with automatic remediation, it will again update or delete the outside security group, and so on\.

To avoid conflicts like these, create configurations that are mutually exclusive, between Firewall Manager and any outside sources\. 

You can use tagging to exclude outside security groups from automatic remediation by your Firewall Manager policies\. To do this, add one or more tags to the security groups or other resources that are managed by the outside source\. Then, when you define the Firewall Manager policy scope, in your resources specification, exclude resources that have the tag or tags that you've added\. 

Similarly, in your outside tool or service, exclude the security groups that Firewall Manager manages from any management or auditing activities\. Either don't import the Firewall Manager resources or use Firewall Manager\-specific tagging to exclude them from outside management\.

## Security group policy limitations<a name="security-groups-limitations"></a>

 This section lists the limitations for using AWS Firewall Manager security group policies:
+ Updating security groups for Amazon EC2 elastic network interfaces that were created using the Fargate service type is not supported\. You can, however, update security groups for Amazon ECS elastic network interfaces with the Amazon EC2 service type\. 
+ Updating Amazon ECS elastic network interfaces is possible only for Amazon ECS services that use the rolling update \(Amazon ECS\) deployment controller\. For other Amazon ECS deployment controllers such as CODE\_DEPLOY or external controllers, Firewall Manager currently can't update the elastic network interfaces\. 
+ Firewall Manager doesn't support updating security groups in elastic network interfaces for Network Load Balancers\. 
+ Firewall Manager doesn’t support security group references in common security group policies\. 

## Security group policy use cases<a name="security-group-policies-use-cases"></a>

You can use AWS Firewall Manager common security group policies to automate the host firewall configuration for communication between Amazon VPC instances\. This section lists standard Amazon VPC architectures and describes how to secure each using Firewall Manager common security group policies\. These security group policies can help you apply a unified set of rules to select resources in different accounts and avoid per\-account configurations in Amazon Elastic Compute Cloud and Amazon VPC\. 

With Firewall Manager common security group policies, you can tag just the EC2 elastic network interfaces that you need for communication with instances in another Amazon VPC\. The other instances in the same Amazon VPC are then more secure and isolated\. 

**Use case: Monitoring and controlling requests to Application Load Balancers and Classic Load Balancers**  
You can use a Firewall Manager common security group policy to define which requests your in\-scope load balancers should serve\. You can configure this through the Firewall Manager console\. Only requests that comply with the security group's inbound rules can reach your load balancers, and the load balancers will only distribute requests that meet the outbound rules\. 

**Use case: Internet\-accessible, public Amazon VPC**  
You can use a Firewall Manager common security group policy to secure a public Amazon VPC, for example, to allow only inbound port 443\. This is the same as only allowing inbound HTTPS traffic for a public VPC\. You can tag public resources within the VPC \(for example, as "PublicVPC"\), and then set the Firewall Manager policy scope to only resources with that tag\. Firewall Manager automatically applies the policy to those resources\.

**Use case: Public and Private Amazon VPC instances**  
You can use the same common security group policy for public resources as recommended in the prior use case for internet\-accessible, public Amazon VPC instances\. You can use a second common security group policy to limit communication between the public resources and the private ones\. Tag the resources in the public and private Amazon VPC instances with something like "PublicPrivate" to apply the second policy to them\. You can use a third policy to define the allowed communication between the private resources and other corporation or private Amazon VPC instances\. For this policy, you can use another identifying tag on the private resources\. 

**Use case: Hub and spoke Amazon VPC instances**  
You can use a common security group policy to define communications between the hub Amazon VPC instance and spoke Amazon VPC instances\. You can use a second policy to define communication from each spoke Amazon VPC instance to the hub Amazon VPC instance\. 

**Use case: Default network interface for Amazon EC2 instances**  
You can use a common security group policy to allow only standard communications, for example internal SSH and patch/OS update services, and to disallow other insecure communication\. 

**Use case: Identify resources with open permissions**  
You can use an audit security group policy to identify all resources within your organization that have permission to communicate with public IP addresses or that have IP addresses that belong to third\-party vendors\.