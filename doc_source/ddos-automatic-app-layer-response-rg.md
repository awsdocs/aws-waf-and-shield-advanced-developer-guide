# The Shield Advanced rule group reference statement<a name="ddos-automatic-app-layer-response-rg"></a>

Shield Advanced manages automatic application layer DDoS mitigation activities using a rule group in the web ACL that you have associated with your resource\. 

The Shield Advanced rule group reference statement in your web ACL has following properties:
+ **Name** – `ShieldMitigationRuleGroup``_account-id_web-acl-id_unique-identifier`
+ **Web ACL capacity units \(WCU\)** – 150\. These WCUs count against the WCU usage in your web ACL\. 
+ **Priority** – 10,000,000\. This high priority setting allows you to run your other rules and rule groups in the web ACL before the Shield Advanced rule group\. AWS WAF runs the rules in a web ACL from the lowest numeric priority setting on up\. 

The automatic mitigation functionality doesn't consume any additional AWS WAF resources in your account, outside of the rule group WCUs in your web ACL\. For example, the Shield Advanced rule group isn't counted as one of your account's rule groups\. For information about account limits in AWS WAF, see [AWS WAF quotas](limits.md)\.