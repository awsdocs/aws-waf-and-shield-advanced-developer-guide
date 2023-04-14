# How AWS WAF works<a name="how-aws-waf-works"></a>

You use AWS WAF to control how your protected resources respond to HTTP\(S\) web requests\. You do this by defining a web access control list \(ACL\) and then associating it with one or more web application resources that you want to protect\. The associated resources forward incoming requests to AWS WAF for inspection by the web ACL\. 

In your web ACL, you create rules to define traffic patterns to look for in requests and to specify the actions to take on matching requests\. The action choices include the following: 
+ Allow the requests to go to the protected resource for processing and response\. 
+ Block the requests\. 
+ Count the requests\. 
+ Run CAPTCHA or challenge checks against requests to verify human users and standard browser use\. 

**Topics**
+ [AWS WAF components](how-aws-waf-works-components.md)
+ [AWS WAF web ACL capacity units \(WCUs\)](aws-waf-capacity-units.md)
+ [Resources that you can protect with AWS WAF](how-aws-waf-works-resources.md)