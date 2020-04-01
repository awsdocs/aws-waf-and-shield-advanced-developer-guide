# SQL injection attack rule statement<a name="waf-rule-statement-type-sqli-match"></a>

Attackers sometimes insert malicious SQL code into web requests in an effort to extract data from your database\. To allow or block web requests that appear to contain malicious SQL code, create one or more SQL injection match conditions\. An SQL injection match condition identifies the part of web requests, such as the URI or the query string, that you want AWS WAF to inspect\. Later in the process, when you create a web ACL, you specify whether to allow or block requests that appear to contain malicious SQL code\.

**Nestable** – You can nest this statement type inside logical rule statements and rate\-based statements\. 

**WCUs** – 20 WCUs\. 

This statement operates on a web request component, and requires the following request component settings: 
+ **Request components** – The part of the web request to inspect, for example, a query string or the body\. For more information, see [Request component](waf-rule-statement-fields.md#waf-rule-statement-request-component)\.
+ **Optional text transformations** – Transformations that you want AWS WAF to perform on the request component before inspecting it\. For example, you could transform to lowercase or normalize white space\. If you specify more than one transformation, AWS WAF processes them in the order listed\. For more information, see [Text transformations](waf-rule-statement-fields.md#waf-rule-statement-transformation)\.

**Where to find this**
+ **Rule builder** on the console – For **Match type**, choose **Attack match conditions** > **Contains SQL injection attacks**\.
+ **API statement** – `SqliMatchStatement`