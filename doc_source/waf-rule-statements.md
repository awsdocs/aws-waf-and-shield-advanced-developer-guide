# AWS WAF rule statements<a name="waf-rule-statements"></a>

Rule statements are the part of a rule that tells AWS WAF how to inspect a web request\. When AWS WAF finds the inspection criteria in a web request, we say that the web request matches the statement\. Every rule statement specifies what to look for and how, according to the statement type\. 

Every rule in AWS WAF has a single top\-level rule statement, which can contain other statements\. Rule statements can be very simple\. For example, you could have a statement that provides a set of originating countries to check your web requests for or you can have a rule statement that just references a rule group\. Rule statements can also be very complex\. For example, you could have a statement that combines many other statements with logical AND, OR, and NOT statements\. 

**Nesting rule statements**  
AWS WAF supports nesting for many rule statements, but not for all\. For example, you can't nest a rule group statement inside of another statement\. You need to use nesting for some scenarios, such as scope\-down statements and logical statements\. The rule statement lists and rule details that follow describe the nesting capabilities and requirements for each category and rule\.

The visual editor for rules in the console supports only one level of nesting for rule statements\. For example, you can nest many types of statements inside a logical AND or OR rule, but you can't nest another AND or OR rule, because that requires a second level of nesting\. To implement multiple levels of nesting, provide the rule definition in JSON, either through the JSON rule editor in the console or through the APIs\. 

**Topics**
+ [Rule statements list](waf-rule-statements-list.md)
+ [Web request components](waf-rule-statement-fields.md)
+ [Statements that reference a set or a rule group](waf-rule-statement-reusable-entities.md)
+ [Scope\-down statements](waf-rule-scope-down-statements.md)
+ [Forwarded IP address](waf-rule-statement-forwarded-ip-address.md)