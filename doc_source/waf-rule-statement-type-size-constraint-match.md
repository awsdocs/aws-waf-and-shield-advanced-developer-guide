# Size constraint rule statement<a name="waf-rule-statement-type-size-constraint-match"></a>

A size constraint statement compares a number of bytes against the size of a request component, using a comparison operator, such as greater than \(>\) or less than \(<\)\. For example, you can use a size constraint statement to look for query strings that are longer than 100 bytes\. 

**Note**  
If you choose **URI** for the value of **Part of the request to filter on**, the **/** in the URI counts as one character\. For example, the URI `/logo.jpg` is nine characters long\.

**Nestable** – You can nest this statement type\. 

**WCUs** – 1 WCU, as a base cost\. If you use the request component **All query parameters**, add 10 WCUs\. If you use the request component **JSON body**, double the base cost WCUs\. For each **Text transformation** that you apply, add 10 WCUs\.

This statement type operates on a web request component, and requires the following request component settings: 
+ **Request components** – The part of the web request to inspect, for example, a query string or the body\.
**Warning**  
If you inspect the request components **Body**, **JSON body**, **Headers**, or **Cookies**, read about the limitations on how much content AWS WAF can inspect at [Handling oversize web request components](waf-oversize-request-components.md)\. 

  For information about web request components, see [Web request components](waf-rule-statement-fields.md)\.
+ **Optional text transformations** – Transformations that you want AWS WAF to perform on the request component before inspecting it\. For example, you could transform to lowercase or normalize white space\. If you specify more than one transformation, AWS WAF processes them in the order listed\. For information, see [Text transformations](waf-rule-statement-transformation.md)\.

Additionally, this statement requires the following settings: 
+ **Size match condition** – This indicates the numerical comparison operator to use to compare the size that you provide with the request component that you've chosen\. Choose the operator from the list\.
+ **Size** – The size setting, in bytes, to use in the comparison\. 

**Where to find this rule statement**
+ **Rule builder** on the console – For **Match type**, under **Size match condition**, choose the condition that you want to use\.
+ **API** – [SizeConstraintStatement](https://docs.aws.amazon.com/waf/latest/APIReference/API_SizeConstraintStatement.html)