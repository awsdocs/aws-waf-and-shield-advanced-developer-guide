# AWS WAF Rule Statements<a name="waf-rule-statements"></a>

Rule statements are the part of a rule that tells AWS WAF how to inspect a web request\. When AWS WAF finds the inspection criteria in a web request, we say that the web request matches the statement\. Every rule statement specifies what to look for and how, according to the statement type\. 

Every rule in AWS WAF has a single top\-level rule statement, which can contain other statements\. Rule statements can be very simple\. For example, you could have a statement that provides just a set of originating countries to check your web requests for\. Rule statements can also be very complex\. For example, you could have a statement that combines many other statements with logical AND, OR, and NOT statements\. 

Web ACLs can also include rule statements that just reference rule groups\. On the console, you don't see these represented as rule statements, but every web ACL has a JSON format representation\. In there, you see these special types of rule statements\. For rules of any complexity, managing your web ACL using the JSON editor is the easiest way to go\. You can retrieve the complete configuration for a web ACL in JSON format, modify it as you need, and then provide it through the console, API, or CLI\. The same holds for rule groups that you manage on your own\.

**Nesting rule statements**  
AWS WAF supports nesting of rule statements\. Some rule statements aren't nestable\. For example, you can't nest a rule group statement inside another statement\. AWS WAF requires nesting for some rule statements\. For example, if you want to control the rate of requests coming from a specific geographical area, you would use a rate\-based rule and nest a geographical match rule inside it, to narrow the scope of the rate tracking\. To combine rule statement results, you nest the statements under logical AND or OR rule statements\. The visual editor on the console supports one level of rule statement nesting, which works for many needs\. To nest more levels, you can edit the JSON representation of the rule on the console\. 

**Topics**
+ [Rule Statements List](waf-rule-statements-list.md)
+ [Request Component Settings](waf-rule-statement-fields.md)
+ [Rule Statements That Reference a Set or a Rule Group](waf-rule-statement-reusable-entities.md)