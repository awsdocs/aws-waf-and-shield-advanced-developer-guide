# Regex pattern set match rule statement<a name="waf-rule-statement-type-regex-pattern-set-match"></a>

The regex pattern set match inspects the part of the web request that you specify for the regular expression patterns that you've specified inside a regex pattern set\.

**Note**  
Each regex pattern set match rule references a regex pattern set, which you create and maintain independent of your rules\. This allows you to use the single set in multiple rules\. When you update the referenced regex pattern set, AWS WAF automatically updates all rules that reference it\.   
For information about creating and managing a regex pattern set, see [Creating and managing a regex pattern set](waf-regex-pattern-set-managing.md)\.

A regex pattern set match statement instructs AWS WAF to search for any of the patterns in the set inside the request component that you choose\. A web request will match the pattern set rule statement if the request component matches any of the patterns in the set\. 

If you want to combine your regex pattern matches using logic, for example to match against some regular expressions and not match against others, consider using [Regex match rule statement](waf-rule-statement-type-regex-match.md)\. 

**Nestable** – You can nest this statement type\. 

**WCUs** – 25 WCUs, as a base cost\. If you use the request component **All query parameters**, add 10 WCUs\. If you use the request component **JSON body**, double the base cost WCUs\. For each **Text transformation** that you apply, add 10 WCUs\.

This statement type operates on a web request component, and requires the following request component settings: 
+ **Request components** – The part of the web request to inspect, for example, a query string or the body\.
**Warning**  
If you inspect the request components **Body**, **JSON body**, **Headers**, or **Cookies**, read about the limitations on how much content AWS WAF can inspect at [Oversize handling for request components](waf-rule-statement-oversize-handling.md)\.

  For information about web request components, see [Web request components](waf-rule-statement-fields.md)\.
+ **Optional text transformations** – Transformations that you want AWS WAF to perform on the request component before inspecting it\. For example, you could transform to lowercase or normalize white space\. If you specify more than one transformation, AWS WAF processes them in the order listed\. For information, see [Text transformations](waf-rule-statement-transformation.md)\.

This statement requires the following settings: 
+ Regex pattern set specification – Choose the regex pattern set that you want to use from the list or create a new one\. 

**Where to find this**
+ **Rule builder** on the console – For **Match type**, choose **String match condition** > **Matches pattern from regular expression set**\.
+ **API statement** – `RegexPatternSetReferenceStatement`