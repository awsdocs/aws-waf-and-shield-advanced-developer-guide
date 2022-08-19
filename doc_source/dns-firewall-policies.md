# Amazon Route 53 Resolver DNS Firewall policies<a name="dns-firewall-policies"></a>

You can use AWS Firewall Manager DNS Firewall policies to manage associations between Amazon Route 53 Resolver DNS Firewall rule groups and your Amazon Virtual Private Cloud *VPCs* across your *organization* in AWS Organizations\. You can apply centrally controlled rule groups to your entire organization, or to a select subset of your accounts and VPCs\. 

DNS Firewall provides filtering and regulation of outbound DNS traffic for your VPCs\. You create reusable collections of filtering rules in DNS Firewall rule groups and you associate the rule groups to your VPCs\. When you apply the Firewall Manager policy, for each account and VPC that's within policy scope, Firewall Manager creates an association between each DNS Firewall rule group in the policy and each VPC that's within scope of the policy, using the association priority settings that you specify in the Firewall Manager policy\. 

For information about using DNS Firewall, see [Amazon Route 53 Resolver DNS Firewall](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver-dns-firewall.html) in the [Amazon Route 53 Developer Guide](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/Welcome.html)\.

The following sections cover requirements for using Firewall Manager DNS Firewall policies and describe how the policies work\. For the procedure for creating the policy, see [Creating an AWS Firewall Manager policy for Amazon Route 53 Resolver DNS Firewall](create-policy.md#creating-firewall-manager-policy-for-dns-firewall)\. 

**You must enable resource sharing**  
A DNS Firewall policy shares DNS Firewall rule groups across the accounts in your organization\. For this to work, you must have resource sharing enabled with AWS Organizations\. For information about how to enable resource sharing, see [Resource sharing for Network Firewall and DNS Firewall policies](resource-sharing.md)\.

**You must have your DNS Firewall rule groups defined**  
When you specify a new DNS Firewall policy, you define the rule groups the same as you do when you're using Amazon Route 53 Resolver DNS Firewall directly\. Your rule groups must already exist in the Firewall Manager administrator account for you to include them in the policy\. For information about creating DNS Firewall rule groups, see [DNS Firewall rule groups and rules](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver-dns-firewall-rule-groups.html)\.

**You define the lowest and highest priority rule group associations**  
The DNS Firewall rule group associations that you manage through Firewall Manager DNS Firewall policies contain the lowest priority associations and the highest priority associations for your VPCs\. In your policy configuration, these appear as first and last rule groups\. 

DNS Firewall filters DNS traffic for the VPC in the following order: 

1. First rule groups, defined by you in the Firewall Manager DNS Firewall policy\. Valid values are between 1 and 99\.

1. DNS Firewall rule groups that are associated by individual account managers through DNS Firewall\. 

1. Last rule groups, defined by you in the Firewall Manager DNS Firewall policy\. Valid values are between 9901 and 10000\.

**How Firewall Manager names the rule group associations that it creates**  
When you save the DNS Firewall policy, if you enabled autoremediation, Firewall Manager creates a DNS Firewall association between the rule groups that you provided in the policy and the VPCs that are in scope of the policy\. Firewall Manager names these associations by concatenating the following values: 
+ The fixed string, `FMManaged_`\.
+ The Firewall Manager policy ID\. This is the AWS resource ID for the Firewall Manager policy\.

The following shows an example name for a firewall that's managed by Firewall Manager:

```
FMManaged_EXAMPLEDNSFirewallPolicyId
```

After you create the policy, if account owners in the VPCs override your firewall policy settings or your rule group associations then Firewall Manager will mark the policy as non\-compliant and try to propose a remedial action\. Account owners can associate other DNS Firewall rule groups to the VPCs that are in scope of the DNS Firewall policy\. Any associations that are created by the individual account owners must have priority settings between your first and last rule group associations\. 