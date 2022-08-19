# IP sets and regex pattern sets<a name="waf-referenced-set-managing"></a>

AWS WAF stores some more complex information in sets that you use by referencing them in your rules\. Each of these sets has a name and is assigned an Amazon Resource Name \(ARN\) at creation\. You can manage these sets from inside your rule statements and you can access and manage them on their own, through the console navigation pane\. 

**Temporary inconsistencies during updates**  
When you create or change a web ACL or other AWS WAF resources, the changes take a small amount of time to propagate to all areas where the resources are stored\. The propagation time can be from a few seconds to a number of minutes\. 

The following are examples of the temporary inconsistencies that you might notice during change propagation: 
+ After you create a web ACL, if you try to associate it with a resource, you might get an exception indicating that the web ACL is unavailable\. 
+ After you add a rule group to a web ACL, the new rule group rules might be in effect in one area where the web ACL is used and not in another\.
+ After you change a rule action setting, you might see the old action in some places and the new action in others\. 
+ After you add an IP address to an IP set that is in use in a blocking rule, the new address might be blocked in one area while still allowed in another\.

**Topics**
+ [Creating and managing an IP set](waf-ip-set-managing.md)
+ [Creating and managing a regex pattern set](waf-regex-pattern-set-managing.md)