# AWS Firewall Manager quotas<a name="fms-limits"></a>

AWS Firewall Manager is subject to the following quotas \(formerly referred to as limits\)\. 

AWS Firewall Manager has default quotas that you might be able to increase and fixed quotas\.

The security group policies managed by Firewall Manager are subject to standard Amazon VPC quotas\. For more information, see [Amazon VPC Quotas](https://docs.aws.amazon.com/vpc/latest/userguide/amazon-vpc-limits.html) in the [Amazon VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/)\. 

Each Firewall Manager Network Firewall policy creates a Network Firewall firewall with an associated firewall policy and its rule groups\. These Network Firewall resources are subject to the quotas listed at [AWS Network Firewall quotas](https://docs.aws.amazon.com/network-firewall/latest/developerguide/quotas.html) in the *Network Firewall Developer Guide*\. 

## Mutable quotas<a name="fms-limits-mutable"></a>

AWS Firewall Manager has default quotas on the number of entities per account\. You can [request an increase](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-waf) in these quotas\.


**All policy types**  

| Resource | Default quota | 
| --- | --- | 
| Accounts per organization in AWS Organizations | Varies\. An invitation sent to an account counts against this quota\. The count is returned if the invited account declines, the management account cancels the invitation, or the invitation expires\. | 
| Firewall Manager policies per organization in AWS Organizations per Region | 20\. The Region specifications `Global` and `US East (N. Virginia)` refer to the same Region, so this limit applies to the total combined policies for the two of them\.  | 
| Organizational units in scope per Firewall Manager policy per Region | 20  | 
| Accounts in scope of a Firewall Manager policy per Region if you explicitly include and exclude individual accounts | 200  | 
| Accounts in scope of a Firewall Manager policy per Region if you do not explicitly include or exclude individual accounts | 2,500  | 
|  Tags that include or exclude resources per Firewall Manager policy  | 8 | 


**Common security group policies**  

| Resource | Default quota | 
| --- | --- | 
| Primary security groups per common Firewall Manager policy | 1 | 
| Amazon VPC instances in scope per Firewall Manager common security group policy, including shared VPCs | 10 | 


**Content audit security group policies**  

| Resource | Default quota | 
| --- | --- | 
| Audit security groups per content audit Firewall Manager policy | 1 | 
| Applications per application list | 50 | 
| Custom managed application lists for any setting in a content audit security group policy | 1 | 
| Custom managed application lists per account | 10 | 
| Protocols per protocol list | 5 | 
| Custom managed protocol lists for any setting in a content audit security group policy | 1 | 
| Custom managed protocol lists per account | 10 | 


**AWS WAF policies**  

| Resource | Default quota | 
| --- | --- | 
| AWS WAF rule groups per Firewall Manager administrator account | 100 | 
| AWS WAF Classic rule groups per Firewall Manager administrator account | 10 | 
| Rule groups per AWS WAF policy | 50 | 
| Total web ACL capacity units \(WCU\) for the rule groups in an AWS WAF policy\. | 1500 | 

## Immutable quotas<a name="fms-limits-immutable"></a>

The following quotas related to AWS Firewall Manager can't be changed\.


**Network Firewall policies**  

| Resource | Quota | 
| --- | --- | 
|  Number of VPCs that can be automatically remediated for a single Network Firewall policy\.  | 1,000 | 
|  The number of IPV4 CIDRs that you can provide for a single Network Firewall policy\.  | 50 | 


**Security group content audit policies**  

| Resource | Quota | 
| --- | --- | 
| Firewall Manager managed application lists for any setting in a content audit security group policy | 1 | 
| Firewall Manager managed protocol lists for any setting in a content audit security group policy | 1 | 


**AWS WAF Classic policies**  

| Resource | Quota | 
| --- | --- | 
| AWS WAF Classic rule groups per Firewall Manager AWS WAF Classic policy | 2: 1 customer\-created rule group and 1 AWS Marketplace rule group | 
| AWS WAF Classic rules per Firewall Manager AWS WAF Classic rule group | 10 | 