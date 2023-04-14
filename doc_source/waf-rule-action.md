# AWS WAF rule action<a name="waf-rule-action"></a>

The rule action tells AWS WAF what to do with a web request when it matches the criteria defined in the rule\. You can optionally add custom behavior to each rule action\. 

**Note**  
Rule actions can be terminating or non\-terminating\. A terminating action stops the web ACL evaluation of the request and either lets it continue to your protected application or blocks it\. 

Here are the rule action options: 
+ **Allow** – AWS WAF allows the request to be forwarded to the protected AWS resource for processing and response\. This is a terminating action\. In rules that you define, you can insert custom headers into the request before forwarding it to the protected resource\.
+ **Block** – AWS WAF blocks the request\. This is a terminating action\. By default, your protected AWS resource responds with an HTTP `403 (Forbidden)` status code\. In rules that you define, you can customize the response\. When AWS WAF blocks a request, the Block action settings determine the response that the protected resource sends back to the client\. 
+ **Count** – AWS WAF counts the request but does not determine whether to allow it or block it\. This is a non\-terminating action\. AWS WAF continues processing the remaining rules in the web ACL\. In rules that you define, you can insert custom headers into the request and you can add labels that other rules can match against\.
+ **CAPTCHA and Challenge** – AWS WAF uses CAPTCHA puzzles and silent challenges to verify that the request is not coming from a bot, and AWS WAF uses tokens to track recent successful client responses\. 
**Note**  
You are charged additional fees when you use the CAPTCHA or Challenge rule action in one of your rules or as a rule action override in a rule group\. For more information, see [AWS WAF Pricing](http://aws.amazon.com/waf/pricing/)\.

  These rule actions can be terminating or non\-terminating, depending on the state of the token in the request: 
  + **Non\-terminating for valid, unexpired token** – If the token is valid and unexpired according to the configured CAPTCHA or challenge immunity time, AWS WAF handles the request similar to the Count action\. AWS WAF continues to inspect the web request based on the remaining rules in the web ACL\. Similar to the Count configuration, in rules that you define, you can optionally configure these actions with custom headers to insert into the request, and you can add labels that other rules can match against\. 
  + **Terminating with blocked request for invalid or expired token** – If the token is invalid or the indicated timestamp is expired, AWS WAF terminates the inspection of the web request and blocks the request, similar to the Block action\. AWS WAF then responds to the client with an error\. For CAPTCHA, if the request contents indicate that the client browser can handle it, AWS WAF sends a CAPTCHA puzzle in a JavaScript interstitial, which is designed to distinguish human clients from bots\. For the Challenge action, AWS WAF sends a JavaScript interstitial with a silent challenge that is designed to distinguish normal browsers from sessions that are being run by bots\. 

  For additional information, see [CAPTCHA and Challenge actions in AWS WAF](waf-captcha-and-challenge.md)\.

For information about customizing requests and responses, see [Customized web requests and responses in AWS WAF](waf-custom-request-response.md)\.

For information about adding labels to matching requests, see [Labels on web requests](waf-labels.md)\.

For information about how web ACL and rule settings interact, see [Web ACL rule and rule group evaluation](web-acl-processing.md)\. 