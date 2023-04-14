# Working with resource sets in Firewall Manager<a name="fms-resource-sets"></a>

An AWS Firewall Manager *resource set* is a collection of resources, such as firewalls, that you can group together and manage in a Firewall Manager policy\. Resource sets enable members in your organization to have granular control over what resources to manage in a policy\. To use resource sets, create a resource set in the console or using the [PutResourceSet](https://docs.aws.amazon.com/fms/2018-01-01/APIReference/API_PutResourceSet.html) API, then add the resource set to your Firewall Manager policy\.

You can create and manage resource sets for the following resource and security policy types:


| Resource type | Firewall Manager security policy type | 
| --- | --- | 
| AWS Network Firewall \- firewalls | Network Firewall policy \- Use resource sets to import existing firewalls from Network Firewall\. For information about using resource sets in a Network Firewall policy, see the [Importing existing firewalls](network-firewall-policies.md#import-existing-nwfw-firewalls) step in the [Creating an AWS Firewall Manager policy for AWS Network Firewall](create-policy.md#creating-firewall-manager-policy-for-network-firewall) procedure\. | 

The following sections cover requirements for creating and deleting resource sets\.

**Topics**
+ [Considerations when working with resource sets in Firewall Manager](#w299aac15c29c13)
+ [Creating resource sets](fms-creating-resource-set.md)
+ [Deleting a resource set](fms-deleting-resource-set.md)

## Considerations when working with resource sets in Firewall Manager<a name="w299aac15c29c13"></a>

Note the following considerations when working with resource sets

**References to non\-existent resources**  
When you add a resource to a resource set, you create a reference to the resource using an Amazon Resource Name \(ARN\)\. Firewall Manager validates that Amazon Resource Name \(ARN\) is the correct format, but Firewall Manager doesn't check that the referenced resource exists\. If the resource doesn't exist yet passes ARN validation, Firewall Manager includes the resource reference in the resource set\. If a new resource with the same ARN is later created, Firewall Manager applies rule groups from the resource set's associated policy to the new resource\.

**Deleted resources**  
When a resource in a resource set is deleted, the reference to the resource remains in the resource set until it's removed by the Firewall Manager administrator\.

**Resources owned by member account that leaves the AWS Organizations organization**  
If a member account leaves the organization, any references to resources owned by that member account will remain in the resource set but will no longer be managed by any policies the resource set is associated with\.

**Association to multiple policies**  
A resource set can be associated with multiple policies, but not all policy types support multiple policies managing the same resource\. See the documentation for your specific policy type for information about unsupported scenarios\.