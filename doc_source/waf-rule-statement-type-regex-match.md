# Regex match rule statement<a name="waf-rule-statement-type-regex-match"></a>

A regex match statement instructs AWS WAF to match a request component against a single regular expression \(regex\)\. A web request matches the statement if the request component matches the regex that you specify\. 

This statement type is a good alternative to the [Regex pattern set match rule statement](waf-rule-statement-type-regex-pattern-set-match.md) for situations where you want to combine your matching criteria using mathematical logic\. For example, if you want a request component to match against some regex patterns and to not match against others, you can combine the regex match statements using the [AND rule statement](waf-rule-statement-type-and.md) and the [NOT rule statement](waf-rule-statement-type-not.md)\. 

AWS WAF supports the pattern syntax used by the PCRE library `libpcre`\. The library is documented at [PCRE \- Perl Compatible Regular Expressions](http://www.pcre.org/)\. 

**Regex pattern use limitations**  
AWS WAF does not support all constructs of the PCRE library\. For example, it supports some zero\-width assertions, but not all\. We do not have comprehensive list of the constructs that are supported\. However, if you provide a regex pattern that is not valid or use unsupported constructs, the AWS WAF API reports a failure\. 

AWS WAF does not support the following PCRE patterns: 
+ Backreferences and capturing subexpressions
+ Subroutine references and recursive patterns
+ Conditional patterns
+ Backtracking control verbs
+ The \\C single\-byte directive
+ The \\R newline match directive
+ The \\K start of match reset directive
+ Callouts and embedded code
+ Atomic grouping and possessive quantifiers

**Nestable** – You can nest this statement type\. 

**WCUs** – 4 WCUs, as a base cost\. If you use the request component **All query parameters**, add 10 WCUs\. If you use the request component **JSON body**, double the base cost WCUs\. For each **Text transformation** that you apply, add 10 WCUs\.

This statement type operates on a web request component, and requires the following request component settings: 
+ **Request components** – The part of the web request to inspect, for example, a query string or the body\.
**Warning**  
If you inspect the request components **Body**, **JSON body**, **Headers**, or **Cookies**, read about the limitations on how much content AWS WAF can inspect at [Handling oversize web request components](waf-oversize-request-components.md)\. 

  For information about web request components, see [Web request components](waf-rule-statement-fields.md)\.
+ **Optional text transformations** – Transformations that you want AWS WAF to perform on the request component before inspecting it\. For example, you could transform to lowercase or normalize white space\. If you specify more than one transformation, AWS WAF processes them in the order listed\. For information, see [Text transformations](waf-rule-statement-transformation.md)\.

**Where to find this rule statement**
+ **Rule builder** on the console – For **Match type**, choose **Matches regular expression**\.
+ **API** – [RegexMatchStatement](https://docs.aws.amazon.com/waf/latest/APIReference/API_RegexMatchStatement.html)