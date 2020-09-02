# Security group common policy findings<a name="security-group-common-policy-findings"></a>

For information about security group common policies, see [Security group policies](security-group-policies.md)\.

**Resource has misconfigured security group\.**  
Firewall Manager has identified a resource that is missing the Firewall Manager managed security group associations that it should have, according to the Firewall Manager policy\. You can enable Firewall Manager remediation on the policy, which creates the associations according to the policy settings\. 
+ Severity – 70
+ Status settings – PASSED/FAILED
+ Updates – Firewall Manager updates this finding\.

**Firewall Manager replica security group is out of sync with primary security group\.**  
A Firewall Manager replica security group is out of sync with its primary security group, according to their common security group policy\. You can enable Firewall Manager remediation on the policy, which syncs the replica security groups with the primary\.
+ Severity – 80
+ Status settings – PASSED/FAILED
+ Updates – Firewall Manager updates this finding\.