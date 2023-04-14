# SQL injection attack rule statement<a name="waf-rule-statement-type-sqli-match"></a>

An SQL injection rule statement inspects for malicious SQL code\. Attackers insert malicious SQL code into web requests in order to do things like modify your database or extract data from it\.

**Nestable** – You can nest this statement type\. 

**WCUs** – The base cost depends on the sensitivity level setting for the rule statement: Low costs 20 and High costs 30\. 

If you use the request component **All query parameters**, add 10 WCUs\. If you use the request component **JSON body**, double the base cost WCUs\. For each **Text transformation** that you apply, add 10 WCUs\.

This statement type operates on a web request component, and requires the following request component settings: 
+ **Request components** – The part of the web request to inspect, for example, a query string or the body\.
**Warning**  
If you inspect the request components **Body**, **JSON body**, **Headers**, or **Cookies**, read about the limitations on how much content AWS WAF can inspect at [Handling oversize web request components](waf-oversize-request-components.md)\. 

  For information about web request components, see [Web request components](waf-rule-statement-fields.md)\.
+ **Optional text transformations** – Transformations that you want AWS WAF to perform on the request component before inspecting it\. For example, you could transform to lowercase or normalize white space\. If you specify more than one transformation, AWS WAF processes them in the order listed\. For information, see [Text transformations](waf-rule-statement-transformation.md)\.

Additionally, this statement requires the following setting: 
+ **Sensitivity level** – This setting tunes the sensitivity of the SQL injection match criteria\. The options are LOW and HIGH\. The default setting is LOW\. 

  The HIGH setting detects more SQL injection attacks, and is the recommended setting\. Due to the higher sensitivity, this setting generates more false positives, especially if your web requests typically contain unusual strings\. During your web ACL testing and tuning, you might need to do more work to mitigate false positives\. For information, see [Testing and tuning your AWS WAF protections](web-acl-testing.md)\. 

  The lower setting provides less stringent SQL injection detection, which also results in fewer false positives\. LOW can be a better choice for resources that have other protections against SQL injection attacks or that have a low tolerance for false positives\. 

**Where to find this rule statement**
+ **Rule builder** on the console – For **Match type**, choose **Attack match condition** > **Contains SQL injection attacks**\.
+ **API** – [SqliMatchStatement](https://docs.aws.amazon.com/waf/latest/APIReference/API_SqliMatchStatement.html)