# AWS Network Firewall policies<a name="network-firewall-policies"></a>

You can use AWS Firewall Manager Network Firewall *policies* to manage AWS Network Firewall *firewalls* for your Amazon Virtual Private Cloud *VPCs* across your *organization* in AWS Organizations\. You can apply centrally controlled firewalls to your entire organization or to a select subset of your accounts and VPCs\. 

Network Firewall provides network traffic filtering protections for the public subnets in your VPCs\. When you apply the Firewall Manager policy, for each account and VPC that's within policy scope, Firewall Manager creates a Network Firewall firewall and deploys firewall endpoints to VPC subnets, to filter network traffic\. 

**Note**  
Firewall Manager Network Firewall policies are Firewall Manager policies that you use to manage Network Firewall protections for your VPCs across your organization\.   
The Network Firewall protections are specified in resources in the Network Firewall service that are called firewall policies\. 

For information about using Network Firewall, see the [AWS Network Firewall Developer Guide](https://docs.aws.amazon.com/network-firewall/latest/developerguide/what-is-aws-network-firewall.html)\.

The following sections cover requirements for using Firewall Manager Network Firewall policies and describe how the policies work\. For the procedure for creating the policy, see [Creating an AWS Firewall Manager policy for AWS Network Firewall](create-policy.md#creating-firewall-manager-policy-for-network-firewall)\. 

**You must enable resource sharing**  
A Network Firewall policy shares Network Firewall rule groups across the accounts in your organization\. For this to work, you must have resource sharing enabled for AWS Organizations\. For information about how to enable resource sharing, see [Resource sharing for Network Firewall and DNS Firewall policies](resource-sharing.md)\.

**You must have your Network Firewall rule groups defined**  
When you specify a new Network Firewall policy, you define the firewall policy the same as you do when you're using AWS Network Firewall directly\. You specify the stateless rule groups to add, default stateless actions, and stateful rule groups\. Your rule groups must already exist in the Firewall Manager administrator account for you to include them in the policy\. For information about creating Network Firewall rule groups, see [AWS Network Firewall rule groups](https://docs.aws.amazon.com/network-firewall/latest/developerguide/rule-groups.html)\.

**How Firewall Manager creates firewall endpoints**  
Depending on how you configure the policy, Firewall Manager creates a single firewall endpoint or multiple firewall endpoints, for each VPC that's within scope\. 
+ For multiple firewall endpoints, Firewall Manager deploys a firewall endpoint in each Availability Zone where you have public\-facing resources in the VPC\. This is the default option for a Network Firewall policy\.
+ For a single firewall endpoint, Firewall Manager deploys a firewall endpoint in a single Availability Zone for the VPC\. With this option, traffic in other zones needs to cross zone boundaries in order to be filtered by the firewall\. 

**How Firewall Manager manages your firewall subnets**  
Firewall subnets are the VPC subnets that Firewall Manager creates for the firewall endpoints that filter your network traffic\. Each firewall endpoint must be deployed in a dedicated VPC subnet\. Firewall Manager creates at least one firewall subnet in each VPC that's within scope of the policy\. 

Firewall Manager only creates firewall subnets in Availability Zones that have public subnets\. A pubic subnet is a subnet attached to an internet gateway\. For more information, see [VPCs and subnets](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html#vpc-subnet-basics) in the [Amazon VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/)\. 

When you first define a Network Firewall policy, you choose one of the following ways for Firewall Manager to manage the firewall subnets in each of the VPCs that are in scope\. You cannot change this choice later\.
+ Deploy a firewall subnet for every Availability Zone that has public subnets\. This is the default behavior\. This provides high availability of your traffic filtering protections\. 
+ Deploy a single firewall subnet in one Availability Zone\. With this choice, Firewall Manager identifies a zone in the VPC that has the most public subnets and creates the firewall subnet there\. The single firewall endpoint filters all network traffic for the VPC\. This can reduce firewall costs, but it isn't highly available and it requires traffic from other zones to cross zone boundaries in order to be filtered\. 

You can provide VPC CIDR blocks for Firewall Manager to use for the firewall subnets or you can leave the choice of firewall endpoint addresses up to Firewall Manager to determine\. 
+ If you don't provide CIDR blocks, Firewall Manager queries your VPCs for available IP addresses to use\. 
+ If you provide a list of CIDR blocks, Firewall Manager restricts its address search for new subnets to your CIDR blocks\. Your CIDR blocks must be /28 CIDR blocks\. For each firewall subnet that Firewall Manager creates, it walks your CIDR block list and uses the first one that it finds that is applicable to the Availability Zone and VPC and has available addresses\. 

If Firewall Manager is unable to create a required firewall subnet in an Availability Zone, it doesn't deploy a firewall endpoint to that zone\. In this case, Firewall Manager marks the VPC as non compliant with the policy\. While the zone is in this state, traffic for the zone must cross zone boundaries in order to be filtered by an endpoint in another zone\. This is similar to the single firewall subnet scenario described previously\. 

**How Firewall Manager manages your Network Firewall resources**  
When you define the policy in Firewall Manager, you provide the network traffic filtering behavior of a standard AWS Network Firewall firewall policy\. You add stateless and stateful Network Firewall rule groups and specify default actions for packets that don’t match any stateless rules\. For information on working with firewall policies in AWS Network Firewall, see the [AWS Network Firewall firewall policies](https://docs.aws.amazon.com/network-firewall/latest/developerguide/firewall-policies.html)\.

When you save the Network Firewall policy, Firewall Manager creates a firewall and firewall policy in each VPC that's within scope of the policy\. Firewall Manager names these Network Firewall resources by concatenating the following values: 
+ A fixed string, either `FMManagedNetworkFirewall` or `FMManagedNetworkFirewallPolicy`, depending on the resource type\.
+ Firewall Manager policy name\. This is the name you assign when you create the policy\.
+ Firewall Manager policy ID\. This is the AWS resource ID for the Firewall Manager policy\.
+ Amazon VPC ID\. This is the AWS resource ID for the VPC where Firewall Manager creates the firewall and firewall policy\.

The following shows an example name for a firewall that's managed by Firewall Manager:

```
FMManagedNetworkFirewallEXAMPLENameEXAMPLEFirewallManagerPolicyIdEXAMPLEVPCId
```

The following shows an example firewall policy name:

```
FMManagedNetworkFirewallPolicyEXAMPLENameEXAMPLEFirewallManagerPolicyIdEXAMPLEVPCId
```

After you create the policy, account owners in the VPCs can't override your firewall policy settings or your rule groups, but they can add rule groups to the firewall policy that Firewall Manager has created\. 

**You must manage your VPC route tables**

When Firewall Manager creates your firewall endpoints, it also creates the VPC route tables for them\. However, Firewall Manager doesn't manage your VPC route tables\. You must configure your VPC route tables to direct network traffic to the firewall endpoints that are created by Firewall Manager\. Using Amazon VPC ingress routing enhancements, change your routing tables to route traffic through the new firewall endpoints\. Your changes must insert the firewall endpoints between the subnets that you want to protect and outside locations\. The exact routing that you need to do depends on your architecture and its components\. 

For information about managing route tables for your VPC, see [Route tables](https://alpha-docs-aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html) in the *Amazon Virtual Private Cloud User Guide*\. For information about managing your route tables for Network Firewall, see [Route table configurations for AWS Network Firewall](https://docs.aws.amazon.com/network-firewall/latest/developerguide/route-tables.html) in the *AWS Network Firewall Developer Guide*\.