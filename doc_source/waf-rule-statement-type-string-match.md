# String match rule statement<a name="waf-rule-statement-type-string-match"></a>

A string match statement indicates the string that you want AWS WAF to search for in a request, where in the request to search, and how\. For example, you can look for a specific string at the start of any query string in the request or as an exact match for the request's `User-agent` header\. Usually, the string consists of printable ASCII characters, but you can use any character from hexadecimal 0x00 to 0xFF \(decimal 0 to 255\)\. 

**Nestable** – You can nest this statement type\. 

**WCUs** – The base cost depends on the type of match that you use\.
+ **Exactly matches string** – 2 
+ **Starts with string** – 2 
+ **Ends with string** – 2 
+ **Contains string** – 10 
+ **Contains word** – 10 

If you use the request component **All query parameters**, add 10 WCUs\. If you use the request component **JSON body**, double the base cost WCUs\. For each **Text transformation** that you apply, add 10 WCUs\.

This statement type operates on a web request component, and requires the following request component settings: 
+ **Request components** – The part of the web request to inspect, for example, a query string or the body\.
**Warning**  
If you inspect the request components **Body**, **JSON body**, **Headers**, or **Cookies**, read about the limitations on how much content AWS WAF can inspect at [Handling oversize web request components](waf-oversize-request-components.md)\. 

  For information about web request components, see [Web request components](waf-rule-statement-fields.md)\.
+ **Optional text transformations** – Transformations that you want AWS WAF to perform on the request component before inspecting it\. For example, you could transform to lowercase or normalize white space\. If you specify more than one transformation, AWS WAF processes them in the order listed\. For information, see [Text transformations](waf-rule-statement-transformation.md)\.

Additionally, this statement requires the following settings: 
+ **String to match** – This is the string that you want AWS WAF to compare to the specified request component\. Usually, the string consists of printable ASCII characters, but you can use any character from hexadecimal 0x00 to 0xFF \(decimal 0 to 255\)\.
+ **String match condition** – This indicates the search type that you want AWS WAF to perform\. 
  + **Exactly matches string** – The string and the value of the request component are identical\.
  + **Starts with string** – The string appears at the beginning of the request component\. 
  + **Ends with string** – The string appears at the end of the request component\. 
  + **Contains string** – The string appears anywhere in the request component\. 
  + **Contains word** – The string that you specify must appear in the request component\. For this option, the string that you specify must contain only alphanumeric characters or underscore \(A\-Z, a\-z, 0\-9, or \_\)\. 

    One of the following must be true for the request to match: 
    + The string exactly matches the value of the request component, such as the value of a header\.
    + The string is at the beginning of the request component and is followed by a character other than an alphanumeric character or underscore \(\_\), for example, `BadBot;`\.
    + The string is at the end of the request component and is preceded by a character other than an alphanumeric character or underscore \(\_\), for example, `;BadBot`\.
    + The string is in the middle of the request component and is preceded and followed by characters other than alphanumeric characters or underscore \(\_\), for example, `-BadBot;`\.

**Where to find this rule statement**
+ **Rule builder** on the console – For **Match type**, choose **String match condition**, and then fill in the strings that you want to match against\.
+ **API** – [ByteMatchStatement](https://docs.aws.amazon.com/waf/latest/APIReference/API_ByteMatchStatement.html)