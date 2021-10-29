# Rule statements list<a name="waf-rule-statements-list"></a>

This section describes the statements that you can add to a rule and provides some guidelines for calculating web ACL capacity units \(WCU\) usage for each\. For information about WCUs, see [AWS WAF Web ACL capacity units \(WCU\)](how-aws-waf-works.md#aws-waf-capacity-units)\. 

This page groups the rule statements by category, provides a high\-level description for each, and provides a link to a section with more information for the statement type\. 

**Match statements**  
Match statements compare the web request or its origin against conditions that you provide\. For many statements of this type, AWS WAF compares a specific component of the request for matching content\. 

Match statements are nestable\. You can nest them inside logical rule statements and use them in scope\-down statements\. 


| Match Statement | Description | WCUs | 
| --- | --- | --- | 
| [Geographic match](waf-rule-statement-type-geo-match.md) | Inspects the request's country of origin\.  | 1 | 
|  [IP set match](waf-rule-statement-type-ipset-match.md)  |  Inspects the request against a set of IP addresses and address ranges\.   |  1 for most cases\. If you configure the statement to use a header with forwarded IP addresses and specify a position in the header of `Any`, then the WCUs are 5\.  | 
|  [Label match rule statement](waf-rule-statement-type-label-match.md)  |  Inspects the request for labels that have been added by other rules in the same web ACL\.  |  1   | 
| [Regex match rule statement](waf-rule-statement-type-regex-match.md) | Compares a regex pattern against a specified request component\.  | 3, as a base cost\. If you use the request component **All query parameters**, add 10 WCUs\. If you use the request component **JSON body**, double the base cost WCUs\. For each **Text transformation** that you apply, add 10 WCUs\.  | 
|  [Regex pattern set](waf-rule-statement-type-regex-pattern-set-match.md)  |  Compares regex patterns against a specified request component\.   |  25 per pattern set, as a base cost\.  If you use the request component **All query parameters**, add 10 WCUs\. If you use the request component **JSON body**, double the base cost WCUs\. For each **Text transformation** that you apply, add 10 WCUs\.  | 
| [Size constraint](waf-rule-statement-type-size-constraint-match.md) | Checks size constraints against a specified request component\.  | 1, as a base cost\.  If you use the request component **All query parameters**, add 10 WCUs\. If you use the request component **JSON body**, double the base cost WCUs\. For each **Text transformation** that you apply, add 10 WCUs\.  | 
| [SQLi attack](waf-rule-statement-type-sqli-match.md) | Inspects for malicious SQL code in a specified request component\.  | 20, as a base cost\. If you use the request component **All query parameters**, add 10 WCUs\. If you use the request component **JSON body**, double the base cost WCUs\. For each **Text transformation** that you apply, add 10 WCUs\. | 
| [String match](waf-rule-statement-type-string-match.md) | Compares a string to a specified request component\.  |  The base cost depends on the type of string match and is between 1 and 10\. If you use the request component **All query parameters**, add 10 WCUs\. If you use the request component **JSON body**, double the base cost WCUs\. For each **Text transformation** that you apply, add 10 WCUs\.  | 
| [XSS scripting attack](waf-rule-statement-type-xss-match.md) | Inspects for cross\-site scripting attacks in a specified request component\.  | 40, as a base cost\. If you use the request component **All query parameters**, add 10 WCUs\. If you use the request component **JSON body**, double the base cost WCUs\. For each **Text transformation** that you apply, add 10 WCUs\. | 

**Logical rules statements**  
Logical rules statements allow you to combine other statements or negate their results\. Every logical rule statement takes at least one nested statement\.

To logically combine or negate rule statement results, you nest the statements under logical rule statements\. 

**Note**  
The visual editor on the console supports one level of rule statement nesting, which works for many needs\. To nest more levels, edit the JSON representation of the rule on the console or use the APIs\. 

Logical rules statements are nestable\. You can nest them inside other logical rule statements and use them in scope\-down statements\. For information about scope\-down statements, see [Scope\-down statements](waf-rule-scope-down-statements.md)\.


| Logical Statement  | Description | WCUs | 
| --- | --- | --- | 
| [`AND` logic](waf-rule-statement-type-and.md) | Combines nested statements with `AND` logic\. | Based on nested statements | 
|  [`NOT` logic](waf-rule-statement-type-not.md)  |  Negates the results of a nested statement\.  |  Based on nested statement  | 
| [`OR` logic](waf-rule-statement-type-or.md) | Combines nested statements with OR logic\. | Based on nested statements | 

**Complex statements**  
AWS WAF supports rate\-based and rule group statements\. You can't nest these statement types inside other rule statements\. For some of these statements, you can narrow the scope of the requests that they inspect by adding a scope\-down statement\. 






| Statement | Description | WCUs | 
| --- | --- | --- | 
|  [Managed rule group](waf-rule-statement-type-managed-rule-group.md)  |  Runs the rules that are defined in the specified managed rule group\.  You can narrow the scope of requests that you evaluate with the rule group by adding a scope\-down statement\.  You cannot nest a managed rule group statement inside any other statement type\.  |  Defined by the rule group, plus any additional WCUs for the scope\-down statement\.  | 
| [Rule group](waf-rule-statement-type-rule-group.md) | Runs the rules that are defined in a rule group that you manage\.  You cannot nest a rule group statement inside any other statement type\. | You define the WCU limit for the rule group when you create it\. | 
|  [Rate\-based](waf-rule-statement-type-rate-based.md)  |  Tracks the rate of requests from individual IP addresses and temporarily blocks addresses while they are sending too many requests\.  You can narrow the scope of requests that you evaluate with a rate\-based statement by adding a scope\-down statement\.  You cannot nest a rate\-based statement under any rule statement\. You can define a rate\-based statement inside a rule group that you manage\.   |  2, plus any additional WCUs for the scope\-down statement\.  | 