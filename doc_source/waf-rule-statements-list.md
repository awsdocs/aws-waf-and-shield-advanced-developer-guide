# Rule statements list<a name="waf-rule-statements-list"></a>

This section describes the statements that you can add to a rule and provides some guidelines for calculating web ACL capacity units \(WCU\) usage for each\. 

This page groups the rule statements by category, provides a high\-level description for each, and provides a link to a section with more information for the statement type\. 

**Match statements**  
Match statements compare the web request or its origin against conditions that you provide\. For many statements of this type, AWS WAF compares a specific component of the request for matching content\. 


| Match Statement | Description | WCUs | Nestable? | 
| --- | --- | --- | --- | 
| [Geographic match](waf-rule-statement-type-geo-match.md) | Inspects the request's country of origin\.  | 1 | Yes | 
| [IP set match](waf-rule-statement-type-ipset-match.md) | Inspects the request against a set of IP addresses and address ranges\.  | 1 for most cases\. If you configure the statement to use a header with forwarded IP addresses and specify a position in the header of Any, then the WCUs are 5\. | Yes | 
| [Regex pattern set](waf-rule-statement-type-regex-pattern-set-match.md) | Compares regex patterns against a specified request component\.  | 25 per pattern set | Yes | 
| [Size constraint](waf-rule-statement-type-size-constraint-match.md) | Checks size constraints against a specified request component\.  | 1 | Yes | 
| [SQLi attack](waf-rule-statement-type-sqli-match.md) | Inspects for malicious SQL code in a specified request component\.  | 20 | Yes | 
| [String match](waf-rule-statement-type-string-match.md) | Compares a string to a specified request component\.  |  Depends on the type of match  | Yes | 
| [XSS scripting attack](waf-rule-statement-type-xss-match.md) | Inspects for cross\-site scripting attacks in a specified request component\.  | 40 | Yes | 

**Logical rules statements**  
Logical rules statements allow you to combine other statements or negate their results\. Every logical rule statement takes at least one nested statement\.


| Logical Statement  | Description | WCUs | Nestable? | 
| --- | --- | --- | --- | 
| [AND logic](waf-rule-statement-type-and.md) | Combines nested statements with AND logic\. | Based on nested statements | Yes | 
| [NOT logic](waf-rule-statement-type-not.md) | Negates the results of a nested statement\. | Based on nested statement | Yes | 
| [OR logic](waf-rule-statement-type-or.md) | Combines nested statements with OR logic\. | Based on nested statements | Yes | 

**Complex statements**  
AWS WAF supports the following complex statements\. 


| Statement | Description | WCUs | Nestable? | 
| --- | --- | --- | --- | 
| [Rate\-based](waf-rule-statement-type-rate-based.md) | Tracks the rate of requests from individual IP addresses\. You can narrow the scope with a nested statement\. | 2 plus any additional WCUs for a nested statement | No | 
| [Managed rule group](waf-rule-statement-type-managed-rule-group.md) | Runs the rules that are defined in the specified managed rule group\.  | Defined by rule group\. | No | 
| [Rule group](waf-rule-statement-type-rule-group.md) | Runs the rules that are defined in a rule group that you manage\.  | You define this for the rule group when you create it\. | No | 