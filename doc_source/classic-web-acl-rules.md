# Working with rules<a name="classic-web-acl-rules"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

Rules let you precisely target the web requests that you want AWS WAF Classic to allow or block by specifying the exact conditions that you want AWS WAF Classic to watch for\. For example, AWS WAF Classic can watch for the IP addresses that requests originate from, the strings that the requests contain and where the strings appear, and whether the requests appear to contain malicious SQL code\.

**Topics**
+ [Creating a rule and adding conditions](classic-web-acl-rules-creating.md)
+ [Adding and removing conditions in a rule](classic-web-acl-rules-editing.md)
+ [Deleting a rule](classic-web-acl-rules-deleting.md)
+ [AWS marketplace rule groups](classic-waf-managed-rule-groups.md)