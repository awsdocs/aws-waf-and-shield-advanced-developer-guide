# Cross\-site scripting attack rule statement<a name="waf-rule-statement-type-xss-match"></a>

An XSS \(cross\-site scripting\) attack statement inspects for malicious scripts in a web request component\. In an XSS attack, the attacker uses vulnerabilities in a benign website as a vehicle to inject malicious client\-site scripts into other legitimate web browsers\. 

**Nestable** – You can nest this statement type\. 

**WCUs** – 40 WCUs, as a base cost\. If you use the request component **All query parameters**, add 10 WCUs\. If you use the request component **JSON body**, double the base cost WCUs\. For each **Text transformation** that you apply, add 10 WCUs\.

This statement type operates on a web request component, and requires the following request component settings: 
+ **Request components** – The part of the web request to inspect, for example, a query string or the body\.
**Warning**  
If you inspect the request components **Body**, **JSON body**, **Headers**, or **Cookies**, read about the limitations on how much content AWS WAF can inspect at [Handling oversize web request components](waf-oversize-request-components.md)\. 

  For information about web request components, see [Web request components](waf-rule-statement-fields.md)\.
+ **Optional text transformations** – Transformations that you want AWS WAF to perform on the request component before inspecting it\. For example, you could transform to lowercase or normalize white space\. If you specify more than one transformation, AWS WAF processes them in the order listed\. For information, see [Text transformations](waf-rule-statement-transformation.md)\.

**Where to find this rule statement**
+ **Rule builder** on the console – For **Match type**, choose **Attack match condition** > **Contains XSS injection attacks**\.
+ **API** – [XssMatchStatement](https://docs.aws.amazon.com/waf/latest/APIReference/API_XssMatchStatement.html)