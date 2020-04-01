# AWS WAF policy findings<a name="waf-policy-findings"></a>

You can use Firewall Manager AWS WAF policies to apply AWS WAF rule groups to your resources in AWS Organizations\. For more information, see [Working with AWS Firewall Manager policies](working-with-policies.md)\.

**Resource is missing Firewall Manager managed web ACL\.**  
An AWS resource doesn't have the AWS Firewall Manager managed web ACL association in accordance with the Firewall Manager policy\. You can enable Firewall Manager remediation on the policy to correct this\. 
+ Severity – 80
+ Status settings – PASSED/FAILED
+ Updates – If Firewall Manager performs the remediation action, it will update the finding and the severity will lower from `HIGH` to `INFORMATIONAL`\. If you perform the remediation, Firewall Manager will not update the finding\. 

**Firewall Manager managed web ACL has misconfigured rule groups\.**  
The rule groups in a web ACL that's managed by Firewall Manager are not configured correctly, according to the Firewall Manager policy\. This means that the web ACL is missing the rule groups that the policy requires\. You can enable Firewall Manager remediation on the policy to correct this\. 
+ Severity – 80
+ Status settings – PASSED/FAILED
+ Updates – If Firewall Manager performs the remediation action, it will update the finding and the severity will lower from `HIGH` to `INFORMATIONAL`\. If you perform the remediation, Firewall Manager will not update the finding\. 