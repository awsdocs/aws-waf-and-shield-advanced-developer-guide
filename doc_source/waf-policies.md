# How AWS WAF policies work<a name="waf-policies"></a>

A Firewall Manager AWS WAF policy contains the rule groups that you want to apply to your resources\. When you apply the policy, Firewall Manager creates a Firewall Manager web ACL in each account that's within policy scope\. Then, the individual account managers can add rules and rule groups to the resulting web ACL, in addition to the rule groups that you have defined\. 

The web ACLs that are managed by Firewall Manager AWS WAF policies contain three sets of rules: 
+ First rule groups, defined by you in the Firewall Manager AWS WAF policy\. 
+ Rules and rule groups that are defined by the account managers in the web ACLs\.
+ Last rule groups, defined by you in the Firewall Manager AWS WAF policy\.

These sets provide a higher level of prioritization for the rules and rule groups in the web ACL\. AWS WAF evaluates the first rule groups, then any account\-managed rules or rule groups, then the last rule groups\. Within each of these sets of rules, AWS WAF evaluates rules and rule groups as usual, according to their priority settings within the set\.

In the policy's first and last rule groups sets, you can only add rule groups\. You can use managed rule groups, which AWS Managed Rules and AWS Marketplace sellers create and maintain for you\. You can also manage and use your own rule groups\. For more information about all of these options, see [Rule groups](waf-rule-groups.md)\.

If you want to use your own rule groups, you create those before you create your Firewall Manager AWS WAF policy\. For guidance, see [Managing your own rule groups](waf-user-created-rule-groups.md)\. To use an individual custom rule, you must define your own rule group and define your rule within that, then use the rule group in your policy\.

For information about how AWS WAF evaluates web requests, see [How AWS WAF processes a Web ACL](web-acl-processing.md)\.

For the procedure to create a Firewall Manager AWS WAF policy, see [Creating an AWS Firewall Manager policy for AWS WAF](create-policy.md#creating-firewall-manager-policy-for-waf)\.