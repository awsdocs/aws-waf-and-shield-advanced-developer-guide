# Working with web ACLs<a name="web-acl-working-with"></a>

When you make changes to web ACLs or web ACL components, like rules and rule groups, AWS WAF propagates the changes everywhere that the web ACL and its components are stored and used\. Your changes are applied within seconds, but there might be a brief period of inconsistency when the changes have arrived in some places and not in others\. So, for example, if you add an IP address to an IP set that's referenced by a blocking rule in a web ACL, the new address might briefly be blocked in one area while still allowed in another\. This temporary inconsistency can occur when you first associate a web ACL with an AWS resource and when you change a web ACL that is already associated with a resource\. Generally, any inconsistencies of this type last only a few seconds\.

**Topics**
+ [Creating a web ACL](web-acl-creating.md)
+ [Associating or disassociating a Web ACL with an AWS resource](web-acl-associating-aws-resource.md)
+ [Editing a Web ACL](web-acl-editing.md)
+ [Deleting a Web ACL](web-acl-deleting.md)
+ [Testing web ACLs](web-acl-testing.md)