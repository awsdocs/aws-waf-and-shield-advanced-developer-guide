# Regex pattern set match rule statement<a name="waf-rule-statement-type-regex-pattern-set-match"></a>

The regex pattern set match inspects the part of the web request that you specify for the regular expression patterns that you've specified inside a regex pattern set\.

**Note**  
Each regex pattern set match rule references a regex pattern set, which you create and maintain independent of your rules\. This allows you to use the single set in multiple rules\. When you update the referenced regex pattern set, AWS WAF automatically updates all rules that reference it\.   
For information about creating and managing a regex pattern set, see [Creating and managing a regex pattern set](waf-regex-pattern-set-managing.md)\.

A regex pattern set match statement instructs AWS WAF to search for any of the patterns in the set inside the request component that you choose\. A web request will match the pattern set rule statement if the request component matches any of the patterns in the set\. 

**Nestable** – You can nest this statement type inside logical rule statements and rate\-based statements\. 

**WCUs** – 25 WCUs per regex pattern set\. 

This statement operates on a web request component, and requires the following request component settings: 
+ **Request components** – The part of the web request to inspect, for example, a query string or the body\. For more information, see [Request component](waf-rule-statement-fields.md#waf-rule-statement-request-component)\.
+ **Optional text transformations** – Transformations that you want AWS WAF to perform on the request component before inspecting it\. For example, you could transform to lowercase or normalize white space\. If you specify more than one transformation, AWS WAF processes them in the order listed\. For more information, see [Text transformations](waf-rule-statement-fields.md#waf-rule-statement-transformation)\.

This statement requires the following settings: 
+ Regex pattern set specification – Choose the regex pattern set that you want to use from the list or create a new one\. 

**Where to find this**
+ **Rule builder** on the console – For **Match type**, choose **String match condition** > **Matches pattern from regular expression set**\.
+ **API statement** – `RegexPatternSetReferenceStatement`