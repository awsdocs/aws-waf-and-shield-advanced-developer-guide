# AWS Firewall Manager policy scope<a name="policy-scope"></a>

Policy scope defines where to apply the policy\. You can apply centrally controlled security group policies to all of your resources and to all of your accounts in your organization in AWS Organizations, or to a select subset of your accounts and resources\. When policies are in place, Firewall Manager manages them continuously, and applies them to new AWS accounts and resources as they are added, according to the policy scope\. 

**AWS accounts in scope**  
The settings that you provide to define the AWS accounts affected by the policy determine which of the accounts in your AWS organization to apply the policy to\. You can choose to apply the policy in one of the following ways: 
+ To all accounts in your organization
+ To only a specific list of included account numbers and AWS Organizations organizational units \(OUs\)
+ To all except a specific list of excluded account numbers and AWS Organizations organizational units \(OUs\)

For information about AWS Organizations, see [AWS Organizations User Guide](https://docs.aws.amazon.com/organizations/latest/userguide/)\. 

Whichever option you choose, when you add a new account to your organization, Firewall Manager automatically assesses it against these settings in each policy and applies the policy as indicated\. For example, if you choose to apply the policy to all accounts except the account numbers in the list, when you add a new account, Firewall Manager applies the policy if the new account number isn't in the exclude list\. 

**Resources for accounts that are removed from policy scope**  
Some resources are not deleted when an account is removed from the policy scope\. To determine which resources should be deleted, Firewall Manager follows these guidelines by default:
+ All AWS Config managed rules are deleted\.
+ Any resource, such as an Application Load Balancer or API from API Gateway, that's associated with a web ACL remains associated with the web ACL\. The web ACL isn't deleted\. 
+ Any resource, such as an Elastic Inference accelerators or Amazon EC2 instance, that uses a replicated security group remains associated with the replicated security group\. The replicated security group isn't deleted\. 

**Resources in scope**  
The settings that you provide for resources determine which resources in the in\-scope accounts and resource types to apply the policy to\. You can choose one of the following: 
+ All resources 
+ All resources except those that have all the tags that you specify
+ Resources that have all the tags that you specify

For more information about tagging your resources, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\. 

Whichever option you choose, when you add a new resource to your account, Firewall Manager automatically assesses the resource against these settings in each policy and applies the policy as indicated\. For example, if you choose to apply the policy only to resources that have all the tags in the list, when you add or update a resource within your policy's account and resource type parameters, Firewall Manager compares the resource's tags to the list and applies the policy if the resource has all the tags\. 