# Rule groups provided by other services<a name="waf-service-owned-rule-groups"></a>

If you or an administrator in your organization uses AWS Firewall Manager or AWS Shield Advanced to manage resource protections using AWS WAF, you might see rule group reference statements added to web ACLs in your account\. 

The names of these rule groups begin with the following strings: 
+ **`ShieldMitigationRuleGroup`** – These rule groups are managed by AWS Shield Advanced\. Shield Advanced adds them to the web ACLs that you use for Shield Advanced application layer \(layer 7\) protections, when you enable automatic application layer DDoS mitigation for the associated resource\. For more information about these rule groups, see [Shield Advanced automatic application layer DDoS mitigation](ddos-automatic-app-layer-response.md)\.
**Warning**  
Don't manually delete this rule group reference statement from your web ACL\. Doing this could have unintended consequences for all resources that are associated with the web ACL\. Instead, use Shield Advanced to disable automatic mitigation for the resources that are associated with the web ACL\. Shield Advanced will remove the rule group when it's not needed for automatic mitigation\.
+ **`PREFMManaged` and `POSTFMManaged`** – These rule groups are managed by AWS Firewall Manager\. Firewall Manager provides them inside web ACLs that Firewall Manager creates and manages\. The names of the web ACLs begin with `FMManagedWebACLV2`\. For information about these web ACLs and rule groups, see [AWS WAF policies](waf-policies.md)\.