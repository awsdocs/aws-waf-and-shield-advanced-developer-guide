# AWS WAF rule statements<a name="waf-rule-statements"></a>

Rule statements are the part of a rule that tells AWS WAF how to inspect a web request\. When AWS WAF finds the inspection criteria in a web request, we say that the web request matches the statement\. Every rule statement specifies what to look for and how, according to the statement type\. 

Every rule in AWS WAF has a single top\-level rule statement, which can contain other statements\. Rule statements can be very simple\. For example, you could have a statement that provides a set of originating countries to check your web requests for\. Rule statements can also be very complex\. For example, you could have a statement that combines many other statements with logical AND, OR, and NOT statements\. 

Web ACLs can also contain rule statements that just reference rule groups\. On the console, you don't see these represented as rule statements, but every web ACL has a JSON format representation\. In the JSON, you can see these special types of rule statements\. For rules of any complexity, managing your web ACL using the JSON editor is the easiest way to go\. You can retrieve the complete configuration for a web ACL in JSON format, modify it as you need, and then provide it to AWS WAF through the console, API, or CLI\. The same is true for rule groups that you manage on your own\.

**Nesting rule statements**  
AWS WAF supports nesting for many rule statements\. You need to use nesting for some scenarios\. For example, to control the rate of requests coming from a specific geographical area, you use a rate\-based rule and nest a geographic match rule inside it, to narrow the scope of the rate tracking\. Some rule statements aren't nestable\. For example, you can't nest a rule group statement inside another statement\. 

To combine rule statement results, you nest the statements under logical AND or OR rule statements\. The visual editor on the console supports one level of rule statement nesting, which works for many needs\. To nest more levels, you can edit the JSON representation of the rule on the console\. 

**Topics**
+ [Rule statements list](waf-rule-statements-list.md)
+ [Request component settings](waf-rule-statement-fields.md)
+ [Forwarded IP address](waf-rule-statement-forwarded-ip-address.md)
+ [Rule statements that reference a set or a rule group](waf-rule-statement-reusable-entities.md)