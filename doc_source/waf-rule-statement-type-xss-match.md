# Cross\-site scripting attack rule statement<a name="waf-rule-statement-type-xss-match"></a>

Attackers sometimes insert scripts into web requests in an effort to exploit vulnerabilities in web applications\. You can create one or more cross\-site scripting match conditions to identify the part of web requests, such as the URI or the query string, that you want AWS WAF to inspect for possible malicious scripts\. 

When you create cross\-site scripting match conditions, you specify filters\. The filters indicate the part of web requests that you want AWS WAF to inspect for malicious scripts, such as the URI or the query string\. You can add more than one filter to a cross\-site scripting match condition, or you can create a separate condition for each filter\. 

**Nestable** – You can nest this statement type inside logical rule statements and rate\-based statements\. 

**WCUs** – 40 WCUs\. 

This statement operates on a web request component, and requires the following request component settings: 
+ **Request components** – The part of the web request to inspect, for example, a query string or the body\. For more information, see [Request component](waf-rule-statement-fields.md#waf-rule-statement-request-component)\.
+ **Optional text transformations** – Transformations that you want AWS WAF to perform on the request component before inspecting it\. For example, you could transform to lowercase or normalize white space\. If you specify more than one transformation, AWS WAF processes them in the order listed\. For more information, see [Text transformations](waf-rule-statement-fields.md#waf-rule-statement-transformation)\.

**Where to find this**
+ **Rule builder** on the console – For **Match type**, choose **Attack match conditions** > **Contains XSS injection attacks**\.
+ **API statement** – `XssMatchStatement`