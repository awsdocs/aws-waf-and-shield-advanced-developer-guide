# Testing and tuning your AWS WAF protections<a name="web-acl-testing"></a>

We recommend that you test and tune any changes to your AWS WAF web ACL before applying them to your website or web application traffic\. 

**Production traffic risk**  
Before you deploy your web ACL implementation for production traffic, test and tune it in a staging or testing environment until you are comfortable with the potential impact to your traffic\. Then test and tune the rules in count mode with your production traffic before enabling them\. 

This section provides guidance for testing and tuning your AWS WAF web ACLs, rules, rule groups, IP sets, and regex pattern sets\.

This section also provides general guidance for testing your use of rule groups that are managed by someone else\. These include AWS Managed Rules rule groups, AWS Marketplace managed rule groups, and rule groups that are shared with you by another account\. For these rule groups, also follow any guidance that you get from the rule group provider\.
+ For the Bot Control AWS Managed Rules rule group, see [Testing and deploying AWS WAF Bot Control](waf-bot-control-deploying.md)\. 
+ For the account takeover prevention AWS Managed Rules rule group, see [Testing and deploying ATP](waf-atp-deploying.md)\. 

**Temporary inconsistencies during updates**  
When you create or change a web ACL or other AWS WAF resources, the changes take a small amount of time to propagate to all areas where the resources are stored\. The propagation time can be from a few seconds to a number of minutes\. 

The following are examples of the temporary inconsistencies that you might notice during change propagation: 
+ After you create a web ACL, if you try to associate it with a resource, you might get an exception indicating that the web ACL is unavailable\. 
+ After you add a rule group to a web ACL, the new rule group rules might be in effect in one area where the web ACL is used and not in another\.
+ After you change a rule action setting, you might see the old action in some places and the new action in others\. 
+ After you add an IP address to an IP set that is in use in a blocking rule, the new address might be blocked in one area while still allowed in another\.