# Creating and managing an IP set<a name="waf-ip-set-managing"></a>

An IP set provides a collection of IP addresses and IP address ranges that you want to use together in a rule statement\. IP sets are AWS resources\. 

To use an IP set in a web ACL or rule group, you first create an AWS resource, `IPSet` with your address specifications\. Then you reference the set when you add an IP set rule statement to a web ACL or rule group\. 

**Topics**
+ [Creating an IP set](waf-ip-set-creating.md)
+ [Using an IP set in a rule group or Web ACL](waf-ip-set-using.md)
+ [Editing an IP set](waf-ip-set-editing.md)
+ [Deleting an IP set](waf-ip-set-deleting.md)