# AWS Firewall Manager policy scope<a name="policy-scope"></a>

The policy scope defines where the policy applies\. You can either apply centrally controlled policies to all of your accounts and resources within your organization in AWS Organizations, or to a subset of your accounts and resources\. For instructions on how to set policy scope, see [Creating an AWS Firewall Manager policy](create-policy.md)\.

## Policy scope options in AWS Firewall Manager<a name="when-in-scope"></a>

When you add a new account or resource to your organization, Firewall Manager automatically assesses it against your settings for each policy and applies the policy based on these settings\. For example, you can choose to apply a policy to all accounts except the account numbers in a specified list; you can also choose to apply a policy only to resources that have all of the tags in a list\. 

**AWS accounts in scope**  
The settings that you provide to define the AWS accounts affected by the policy determine which of the accounts in your AWS organization to apply the policy to\. You can choose to apply the policy in one of the following ways: 
+ To all accounts in your organization
+ To only a specific list of included account numbers and AWS Organizations organizational units \(OUs\)
+ To all except a specific list of excluded account numbers and AWS Organizations organizational units \(OUs\)

For information about AWS Organizations, see [AWS Organizations User Guide](https://docs.aws.amazon.com/organizations/latest/userguide/)\. 

**Resources in scope**  
Similarly to the settings for accounts in scope, the settings that you provide for resources determine which in\-scope resource types to apply the policy to\. You can choose one of the following: 
+ All resources 
+ Resources that have all of the tags that you specify
+ All resources except those that have all of the tags that you specify

For more information about tagging your resources, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\. 

## Policy scope management in AWS Firewall Manager<a name="when-out-of-scope"></a>

When policies are in place, Firewall Manager manages them continuously and applies them to new AWS accounts and resources as they are added, in accordance with the policy scope\. 

**How Firewall Manager manages AWS accounts and resources**  
If an account or resource goes out of scope for any reason, AWS Firewall Manager doesn't automatically remove protections or delete Firewall Manager\-managed resources unless you select the **Automatically remove protections from resources that leave the policy scope** check box\.

**Note**  
**Automatically remove protections from resources that leave the policy scope** is not available for AWS Shield Advanced or AWS WAF Classic policies\.

Selecting this check box directs AWS Firewall Manager to automatically clean up resources that Firewall Manager manages for accounts when those accounts leave the policy scope\. For example, Firewall Manager will disassociate a Firewall Manager\-managed web ACL from a protected customer resource when the customer resource leaves the policy scope\.

To determine which resources should be removed from protection when a customer resource leaves the policy scope, Firewall Manager follows these guidelines:
+ *Default behavior*:
  + The associated AWS Config managed rules are deleted\. This behavior is independent of the check box\.
  + Any protected resource that goes out of scope remains associated and protected\. For example, an Application Load Balancer or API from API Gateway that's associated with a web ACL remains associated with the web ACL, and the protection remains in place\.
+ *With the **Automatically remove protections from resources that leave the policy scope** check box selected*:
  + The associated AWS Config managed rules are deleted\. This behavior is independent of the check box\.
  + Any protected resource that goes out of scope is automatically disassociated and removed from protection when it leaves the policy scope\. For example, an Elastic Inference accelerator or Amazon EC2 instance is automatically disassociated from the replicated security group when it leaves the policy scope\. The replicated security group and its resources are automatically removed from protection\.