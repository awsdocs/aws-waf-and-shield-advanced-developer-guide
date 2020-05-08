# Working with AWS WAF Classic rule groups for use with AWS Firewall Manager<a name="classic-working-with-rule-groups"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

An AWS WAF Classic *rule group* is a set of rules that you add to an AWS WAF Classic AWS Firewall Manager policy\. You can create your own rule group, or you can purchase a managed rule group from AWS Marketplace\. 

**Important**  
If you want to add an AWS Marketplace rule group to your Firewall Manager policy, each account in your organization must first subscribe to that rule group\. After all accounts have subscribed, you can then add the rule group to a policy\. For more information, see [AWS marketplace rule groups](classic-waf-managed-rule-groups.md)\.

**Topics**
+ [Creating an AWS WAF Classic rule group](classic-create-rule-group.md)
+ [Adding and deleting rules from an AWS WAF Classic rule group](classic-rule-group-editing.md)