# AWS Firewall Manager Limits<a name="fms-limits"></a>

AWS Firewall Manager has default limits on the number of entities per account\. You can [request an increase](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-waf) in these limits\.


| Resource | Default Limit | 
| --- | --- | 
| Accounts per organization in AWS Organizations | Varies\. An invitation sent to an account counts against this limit\. The count is returned if the invited account declines, the master account cancels the invitation, or the invitation expires\. | 
| Firewall Manager policies per organization in AWS Organizations | 20 | 
|  Tags that include or exclude resources per Firewall Manager policy  | 8 | 
| Rule groups per Firewall Manager administrator account | 10 | 
| Primary security groups per common Firewall Manager policy | 1 | 
| Audit security groups per content audit Firewall Manager policy | 1 | 
| Amazon VPC instances in scope per Firewall Manager common security group policy | 5 | 

The security group policies managed by Firewall Manager are subject to standard Amazon VPC limits\. For more information, see [Amazon VPC Limits](https://docs.aws.amazon.com/vpc/latest/userguide//amazon-vpc-limits.html) in the [Amazon VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/)\. 

The following limits related to AWS Firewall Manager can't be changed\.


| Resource | Limit | 
| --- | --- | 
| Rule groups per Firewall Manager policy | 2: 1 customer\-created rule group and 1 AWS Marketplace rule group | 
| Rules per rule group | 10 | 