# IP sets and regex pattern sets<a name="waf-referenced-set-managing"></a>

AWS WAF stores some more complex information in sets that you use by referencing them in your rules\. Each of these sets has a name and is assigned an Amazon Resource Name \(ARN\) at creation\. You can manage these sets from inside your rule statements and you can access and manage them on their own, through the console navigation pane\. 

**Eventual consistency**  
When you make changes to web ACLs or web ACL components, like rules and rule groups, AWS WAF propagates the changes everywhere that the web ACL and its components are stored and used\. Your changes are applied within seconds, but there might be a brief period of inconsistency when the changes have arrived in some places and not in others\. So, for example, if you add an IP address to an IP set that's referenced by a blocking rule in a web ACL, the new address might briefly be blocked in one area while still allowed in another\. This temporary inconsistency can occur when you first associate a web ACL with an AWS resource and when you change a web ACL that is already associated with a resource\. Generally, any inconsistencies of this type last only a few seconds\.

**Topics**
+ [Creating and managing an IP set](waf-ip-set-managing.md)
+ [Creating and managing a regex pattern set](waf-regex-pattern-set-managing.md)