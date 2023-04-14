# AWS Network Firewall policies<a name="network-firewall-policies"></a>

You can use AWS Firewall Manager Network Firewall *policies* to manage AWS Network Firewall *firewalls* for your Amazon Virtual Private Cloud *VPCs* across your *organization* in AWS Organizations\. You can apply centrally controlled firewalls to your entire organization or to a select subset of your accounts and VPCs\. 

Network Firewall provides network traffic filtering protections for the public subnets in your VPCs\. Firewall Manager creates and manages your firewalls based on the *firewall management type* defined by your policy\. Firewall Manager provides the following firewall management models:
+ **Distributed** \- For each account and VPC that's within policy scope, Firewall Manager creates a Network Firewall firewall and deploys firewall endpoints to VPC subnets, to filter network traffic\.
+ **Centralized** \- Firewall Manager creates a single Network Firewall firewall in a single Amazon VPC\.
+ **Import existing firewalls** \- Firewall Manager imports existing firewalls for management in a single Firewall Manager policy\. You can apply additional rules to the imported firewalls managed by your policy to ensure that your firewalls meet your security standards\.

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
The *Firewall management type* in your policy determines how Firewall Manager creates firewalls\. Your policy can create *distributed* firewalls, a *centralized* firewall, or you can **import existing firewalls**:
+ **Distributed** \- With the distributed deployment model, Firewall Manager creates endpoints for each VPC that's within policy scope\. You can either customize the endpoint location by specifying which Availability Zones to create firewall endpoints in, or Firewall Manager can automatically create endpoints in the Availability Zones with public subnets\. If you manually choose the Availability Zones, you have the option to restrict the set of allowed CIDRs per Availability Zone\. If you decide to let Firewall Manager automatically create the endpoints, you must also specify whether the service will create a single endpoint or multiple firewall endpoints within your VPCs\.
  + For multiple firewall endpoints, Firewall Manager deploys a firewall endpoint in each Availability Zone where you have a subnet with an internet gateway or a Firewall Manager\-created firewall endpoint route in the route table\. This is the default option for a Network Firewall policy\.
  + For a single firewall endpoint, Firewall Manager deploys a firewall endpoint in a single Availability Zone in any subnet that has an internet gateway route\. With this option, traffic in other zones needs to cross zone boundaries in order to be filtered by the firewall\.
**Note**  
For both of these options, there must be a subnet associated to a route table that has an IPv4/prefixlist route in it\. Firewall Manager does not check for any other resources\.
+ **Centralized** \- With the centralized deployment model, Firewall Manager creates one or more firewall endpoints within an *inspection VPC*\. An inspection VPC is a central VPC where Firewall Manager launches your endpoints\. When you use the centralized deployment model, you also specify which Availability Zones to create firewall endpoints in\. You can't change the inspection VPC after you create your policy\. To use a different inspection VPC, you must create a new policy\.
+ **Import existing firewalls** \- When you import existing firewalls, you choose the firewalls to manage in your policy by adding one or more *resource sets* to your policy\. A resource set is a collection of resources, in this case existing firewalls in Network Firewall, that are managed by an account in your organization\. Before you use resource sets in your policy, you must first create a resource set\. For information about Firewall Manager resource sets, see [Working with resource sets in Firewall Manager](fms-resource-sets.md)\.

  Keep in mind the following considerations when working with imported firewalls:
  + If an imported firewall become non\-compliant, Firewall Manager will try to automatically resolve the violation, except for under the following circumstances:
    + If there's a mismatch between the Firewall Manager and Network Firewall policy's stateful or stateless default actions\.
    + If a rule group in an imported firewall's firewall policy has the same priority as a rule group in the Firewall Manager policy\.
    + If an imported firewall uses a firewall policy that's associated with a firewall that's not part of the policy's resource set\. This can happen because a firewall can have exactly one firewall policy, but a single firewall policy can be associated with multiple firewalls\.
    + If a pre\-existing rule group belonging to an imported firewall's firewall policy that is also specified in the Firewall Manager policy is given a different priority\.
  + If you enable resource cleanup in the policy, Firewall Manager removes the rule groups which have been in FMS import policy from the firewalls in scope of the resource set\.
  + Firewalls managed by that are managed by a Firewall Manager import existing firewall management type can only be managed by one policy at a time\. If the same resource set is added to multiple import network firewall policies, the firewalls in the resource set will be managed by the first policy the resource set was added to and will be ignored by the second policy\.

If you change the list of Availability Zones for policies using distributed or centralized firewall management, Firewall Manager will try to clean up any endpoints that were created in the past, but that aren't currently in policy scope\. Firewall Manager will remove the endpoint only if there are no route table routes that reference the out of scope endpoint\. If Firewall Manager finds that it is unable to delete these endpoints, it will mark the firewall subnet as being non\-compliant and will continue attempting to remove the endpoint until such time as it is safe to delete\.

**How Firewall Manager manages your firewall subnets**  
Firewall subnets are the VPC subnets that Firewall Manager creates for the firewall endpoints that filter your network traffic\. Each firewall endpoint must be deployed in a dedicated VPC subnet\. Firewall Manager creates at least one firewall subnet in each VPC that's within scope of the policy\.

For policies that use the distributed deployment model with automatic endpoint configuration, Firewall Manager only creates firewall subnets in Availability Zones that have a subnet with an internet gateway route, or a subnet with a route to the firewall endpoints that Firewall Manager created for their policy\. For more information, see [VPCs and subnets](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html#vpc-subnet-basics) in the [Amazon VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/)\.

For policies that use either the distributed or centralized model where you specify which Availability Zones Firewall Manager creates the firewall endpoints in, Firewall Manager creates an endpoint in those specific Availability Zones irrespective of whether there are other resources in the Availability Zone\.

When you first define a Network Firewall policy, you specify how Firewall Manager manages the firewall subnets in each of the VPCs that are in scope\. You cannot change this choice later\.

For policies that use the distributed deployment model with automatic endpoint configuration, you can choose between the following options:
+ Deploy a firewall subnet for every Availability Zone that has public subnets\. This is the default behavior\. This provides high availability of your traffic filtering protections\. 
+ Deploy a single firewall subnet in one Availability Zone\. With this choice, Firewall Manager identifies a zone in the VPC that has the most public subnets and creates the firewall subnet there\. The single firewall endpoint filters all network traffic for the VPC\. This can reduce firewall costs, but it isn't highly available and it requires traffic from other zones to cross zone boundaries in order to be filtered\. 

For policies that use distributed deployment model with custom endpoint configuration or the centralized deployment model, Firewall Manager creates the subnets in the specified Availability Zones that are within the policy scope\.

You can provide VPC CIDR blocks for Firewall Manager to use for the firewall subnets or you can leave the choice of firewall endpoint addresses up to Firewall Manager to determine\. 
+ If you don't provide CIDR blocks, Firewall Manager queries your VPCs for available IP addresses to use\. 
+ If you provide a list of CIDR blocks, Firewall Manager searches for new subnets only in the CIDR blocks that you provide\. You must use /28 CIDR blocks\. For each firewall subnet that Firewall Manager creates, it walks your CIDR block list and uses the first one that it finds that is applicable to the Availability Zone and VPC and has available addresses\. If Firewall Manager is unable to find open space in the VPC \(with or without the restriction\), the service won't create a firewall in the VPC\.

If Firewall Manager can't create a required firewall subnet in an Availability Zone, it marks the subnet as non\-compliant with the policy\. While the zone is in this state, traffic for the zone must cross zone boundaries in order to be filtered by an endpoint in another zone\. This is similar to the single firewall subnet scenario\. 

**How Firewall Manager manages your Network Firewall resources**  
When you define the policy in Firewall Manager, you provide the network traffic filtering behavior of a standard AWS Network Firewall firewall policy\. You add stateless and stateful Network Firewall rule groups and specify default actions for packets that don’t match any stateless rules\. For information on working with firewall policies in AWS Network Firewall, see the [AWS Network Firewall firewall policies](https://docs.aws.amazon.com/network-firewall/latest/developerguide/firewall-policies.html)\.

For distributed and centralized policies, when you save the Network Firewall policy, Firewall Manager creates a firewall and firewall policy in each VPC that's within scope of the policy\. Firewall Manager names these Network Firewall resources by concatenating the following values: 
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

After you create the policy, member accounts in the VPCs can't override your firewall policy settings or your rule groups, but they can add rule groups to the firewall policy that Firewall Manager has created\.

**How Firewall Manager manages and monitors VPC route tables for your policy**

**Note**  
Route table management isn't currently supported for policies that use the centralized deployment model\.

When Firewall Manager creates your firewall endpoints, it also creates the VPC route tables for them\. However, Firewall Manager doesn't manage your VPC route tables\. You must configure your VPC route tables to direct network traffic to the firewall endpoints that are created by Firewall Manager\. Using Amazon VPC ingress routing enhancements, change your routing tables to route traffic through the new firewall endpoints\. Your changes must insert the firewall endpoints between the subnets that you want to protect and outside locations\. The exact routing that you need to do depends on your architecture and its components\.

Currently, Firewall Manager allows monitoring of your VPC route table routes for any traffic destined to the internet gateway, that is bypassing the firewall\. Firewall Manager doesn't support other target gateways like NAT gateways\.

For information about managing route tables for your VPC, see [Managing route tables for your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html) in the *Amazon Virtual Private Cloud User Guide*\. For information about managing your route tables for Network Firewall, see [Route table configurations for AWS Network Firewall](https://docs.aws.amazon.com/network-firewall/latest/developerguide/route-tables.html) in the *AWS Network Firewall Developer Guide*\.

When you enable monitoring for a policy, Firewall Manager continuously monitors VPC route configurations and alerts you about traffic that bypasses firewall inspection for that VPC\. If a subnet has a firewall endpoint route, Firewall Manager looks for the following routes:
+ Routes to send traffic to the Network Firewall endpoint\. 
+ Routes to forward the traffic from the Network Firewall endpoint to the internet gateway\. 
+ Inbound routes from the internet gateway to the Network Firewall endpoint\. 
+ Routes from the firewall subnet\.

If a subnet has a Network Firewall route but there's asymmetric routing in Network Firewall and your internet gateway route table, Firewall Manager reports the subnet as non\-compliant\. Firewall Manager also detects routes to the internet gateway in the firewall route table that Firewall Manager created, as well as the route table for your subnet, and reports them as non\-compliant\. Additional routes in the Network Firewall subnet route table and your internet gateway route table are also reported as non\-compliant\. Depending on the violation type, Firewall Manager suggests remediation actions to bring the route configuration into compliance\. Firewall Manager doesn't offer suggestions in all cases\. For example, if your customer subnet has a firewall endpoint that was created outside of Firewall Manager, Firewall Manager doesn't suggest remediation actions\. 

By default, Firewall Manager will mark any traffic that crosses the Availability Zone boundary for inspection as being non\-compliant\. However, if the you choose to automatically create a single endpoint in your VPC, Firewall Manager won't mark traffic that crosses the Availability Zone boundary as non\-compliant\.

For policies that use distributed deployment models with custom endpoint configuration, you can choose whether the traffic crossing the Availability Zone boundary from an Availability Zone without a firewall endpoint is marked as compliant or non\-compliant\.

**Note**  
Firewall Manager does not suggest remediation actions for non\-IPv4 routes, such as IPv6 and prefix list routes\.
Calls made using the `DisassociateRouteTable` API call can take up to 12 hours to detect\.
Firewall Manager creates a Network Firewall route table for a subnet that contains the firewall endpoints\. Firewall Manager assumes that this route table contains only valid internet gateway and VPC default routes\. Any extra or invalid routes in this route table are considered to be non\-compliant\.

When you configure your Firewall Manager policy, if you choose **Monitor** mode, Firewall Manager provides resource violation and remediation details about your resources\. You can use these suggested remediation actions to fix route issues in your route tables\. If you choose **Off** mode, Firewall Manager doesn't monitor your route table content for you\. With this option, you manage your VPC route tables for yourself\. For more information about these resource violations, see [Viewing compliance information for an AWS Firewall Manager policy](fms-compliance.md)\.

**Warning**  
If you choose **Monitor** under** AWS Network Firewall route configuration** when creating your policy, you can't turn it off for that policy\. However, if you choose **Off**, you can enable it later\.

## Configuring logging for an AWS Network Firewall policy<a name="nwfw-policies-logging-config"></a>

You can enable centralized logging for your Network Firewall policies to get detailed information about traffic within your organization\. You can select flow logging to capture network traffic flow, or alert logging to report traffic that matches a rule with the rule action set to `DROP` or `ALERT`\. For more information about AWS Network Firewall logging, see [ Logging network traffic from AWS Network Firewall](https://docs.aws.amazon.com/network-firewall/latest/developerguide/firewall-logging.html) in the *AWS Network Firewall Developer Guide*\. 

You send logs from your policy's Network Firewall firewalls to an Amazon S3 bucket\. After you enable logging, AWS Network Firewall delivers logs for each configured Network Firewall by updating the firewall settings to deliver logs to your selected Amazon S3 buckets with the reserved AWS Firewall Manager prefix, `<policy-name>-<policy-id>`\. 

**Note**  
This prefix is used by Firewall Manager to determine whether a logging configuration was added by Firewall Manager, or whether it was added by the account owner\. If the account owner attempts to use the reserved prefix for their own custom logging, it is overwritten by the logging configuration in the Firewall Manager policy\. 

For more information about how to create an Amazon S3 bucket and review the stored logs, see [ What is Amazon S3?](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html) in the *Amazon Simple Storage Service User Guide*\. 

To enable logging you must meet the following requirements:
+ The Amazon S3 that you specify in your Firewall Manager policy must exist\.
+ You must have the following permissions:
  + `logs:CreateLogDelivery`
  + `s3:GetBucketPolicy`
  + `s3:PutBucketPolicy`
+ If the Amazon S3 bucket that's your logging destination uses server\-side encryption with keys that are stored in AWS Key Management Service, you must add the following policy to your AWS KMS customer\-managed key to allow Firewall Manager to log to your CloudWatch Logs log group:

  ```
  {
      "Effect": "Allow",
      "Principal": {
          "Service": "delivery.logs.amazonaws.com"
      },
      "Action": [
          "kms:Encrypt*",
          "kms:Decrypt*",
          "kms:ReEncrypt*",
          "kms:GenerateDataKey*",
          "kms:Describe*"
      ],
      "Resource": "*"
  }
  ```

Note that only buckets in the Firewall Manager administrator account may be used for AWS Network Firewall central logging\. 

When you enable centralized logging on a Network Firewall policy, Firewall Manager takes these actions on your account: 
+ Firewall Manager updates the permissions on selected S3 buckets to allow for log delivery\. 
+ Firewall Manager creates directories in the S3 bucket for each member account in the scope of the policy\. The logs for each account can be found at `<bucket-name>/<policy-name>-<policy-id>/AWSLogs/<account-id>`\. 

**To enable logging for a Network Firewall policy**

1. Create an Amazon S3 bucket using your Firewall Manager administrator account\. For more information, see [ Creating a bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/create-bucket-overview.html) in the *Amazon Simple Storage Service User Guide*\.

1. Sign in to the AWS Management Console using your Firewall Manager administrator account, and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fmsv2](https://console.aws.amazon.com/wafv2/fmsv2)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [AWS Firewall Manager prerequisites](fms-prereq.md)\.

1. In the navigation pane, choose **Security Policies**\.

1. Choose the Network Firewall policy that you want to enable logging for\. For more information about AWS Network Firewall logging, see [ Logging network traffic from AWS Network Firewall](https://docs.aws.amazon.com/network-firewall/latest/developerguide/firewall-logging.html) in the *AWS Network Firewall Developer Guide*\.

1. On the **Policy details** tab, in the **Policy rules** section, choose **Edit**\.

1. To enable and aggregate logs, choose one or more options under **Logging configuration**:
   + **Enable and aggregate flow logs**
   + **Enable and aggregate alert logs**

1. Choose the Amazon S3 bucket where you want your logs to be delivered\. You must choose a bucket for each log type that you enable\. You can use the same bucket for both log types\.

1. \(Optional\) If you want custom member account\-created logging to be replaced with the policy’s logging configuration, choose **Override existing logging configuration**\.

1. Choose **Next**\.

1. Review your settings, then choose **Save** to save your changes to the policy\.

**To disable logging for a Network Firewall policy**

1. Sign in to the AWS Management Console using your Firewall Manager administrator account, and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fmsv2](https://console.aws.amazon.com/wafv2/fmsv2)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [AWS Firewall Manager prerequisites](fms-prereq.md)\.

1. In the navigation pane, choose **Security Policies**\.

1. Choose the Network Firewall policy that you want to disable logging for\.

1. On the **Policy details** tab, in the **Policy rules** section, choose **Edit**\.

1. Under **Logging configuration status**, deselect **Enable and aggregate flow logs** and **Enable and aggregate alert logs** if they are selected\.

1. Choose **Next**\.

1. Review your settings, then choose **Save** to save your changes to the policy\.