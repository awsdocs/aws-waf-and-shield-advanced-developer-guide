# AWS Shield Advanced policy findings<a name="shield-policy-findings"></a>

You use Firewall Manager Shield policies to protect accounts and resources AWS Shield Advanced\. For more information, see [Working with AWS Firewall Manager policies](working-with-policies.md)\.

**Resource lacks Shield Advanced protection\.**  
An AWS resource that should have Shield Advanced protection, according to the Firewall Manager policy, doesn't have it\. You can enable Firewall Manager remediation on the policy, which will enable the protection for the resource\. 
+ Severity – 60
+ Status settings – PASSED/FAILED
+ Updates – If Firewall Manager performs the remediation action, it will update the finding and the severity will lower from `HIGH` to `INFORMATIONAL`\. If you perform the remediation, Firewall Manager will not update the finding\. 

**Shield Advanced detected attack against monitored resource\.**  
Shield Advanced detected an attack on a protected AWS resource\. You can enable Firewall Manager remediation on the policy\.
+ Severity – 70
+ Status settings – None
+ Updates – Firewall Manager does not update this finding\.