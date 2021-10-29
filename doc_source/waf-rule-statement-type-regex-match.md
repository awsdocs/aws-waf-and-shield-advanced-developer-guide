# Regex match rule statement<a name="waf-rule-statement-type-regex-match"></a>

A regex match statement instructs AWS WAF to match a request component against a single regular expression \(regex\)\. A web request matches the statement if the request component matches the regex that you specify\. 

This statement type is a good alternative to the [Regex pattern set match rule statement](waf-rule-statement-type-regex-pattern-set-match.md) for situations where you want to combine your matching criteria using mathematical logic\. For example, if you want a request component to match against some regex patterns and to not match against anothers, you can combine the regex match statements using the [`AND` rule statement](waf-rule-statement-type-and.md) and the [`NOT` rule statement](waf-rule-statement-type-not.md)\. 

**Nestable** – You can nest this statement type\. 

**WCUs** – 3 WCUs, as a base cost\. If you use the request component **All query parameters**, add 10 WCUs\. If you use the request component **JSON body**, double the base cost WCUs\. For each **Text transformation** that you apply, add 10 WCUs\.

This statement type operates on a web request component, and requires the following request component settings: 
+ **Request components** – The part of the web request to inspect, for example, a query string or the body\.
**Warning**  
If you use the request component **Body** or **JSON body**, AWS WAF only inspects the first 8 KB\. For information, see [Web request body inspection](web-request-body-inspection.md)\.

  For information about web request components, see [Request component](waf-rule-statement-fields.md#waf-rule-statement-request-component)\.
+ **Optional text transformations** – Transformations that you want AWS WAF to perform on the request component before inspecting it\. For example, you could transform to lowercase or normalize white space\. If you specify more than one transformation, AWS WAF processes them in the order listed\. For information, see [Text transformations](waf-rule-statement-fields.md#waf-rule-statement-transformation)\.

**Where to find this**
+ **Rule builder** on the console – For **Match type**, choose **Matches regular expression**\.
+ **API statement** – `RegexMatchStatement`