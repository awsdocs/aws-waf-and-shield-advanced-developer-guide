# Security group usage audit policy findings<a name="security-group-usage-audit-policy-findings"></a>

For information about security group usage audit policies, see [Security group policies](security-group-policies.md)\.

**Firewall Manager found redundant security group\.**  
The Firewall Manager security group usage audit has identified a redundant security group\. This is a security group with an identical rules set as another security group within the same Amazon Virtual Private Cloud instance\. You can enable Firewall Manager automatic remediation on the usage audit policy, which replaces redundant security groups and with a single security group\.
+ Severity – 30
+ Status settings – None
+ Updates – Firewall Manager does not update this finding\.

**Firewall Manager found unused security group\.**  
The Firewall Manager security group usage audit has identified an unused security group\. This is a security group that's not referenced by any Firewall Manager common security group policy\. You can enable Firewall Manager automatic remediation on the usage audit policy, which removes unused security groups\.
+ Severity – 30
+ Status settings – None
+ Updates – Firewall Manager does not update this finding\.