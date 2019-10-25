# How AWS WAF Works<a name="how-aws-waf-works"></a>

You use AWS WAF to control how API Gateway, Amazon CloudFront or an Application Load Balancer responds to web requests\. You start by creating conditions, rules, and web access control lists \(web ACLs\)\. You define your conditions, combine your conditions into rules, and combine the rules into a web ACL\.

**Conditions**  
Conditions define the basic characteristics that you want AWS WAF to watch for in web requests:  
+ Scripts that are likely to be malicious\. Attackers embed scripts that can exploit vulnerabilities in web applications\. This is known as *cross\-site scripting*\.
+ IP addresses or address ranges that requests originate from\.
+ Country or geographical location that requests originate from\.
+ Length of specified parts of the request, such as the query string\.
+ SQL code that is likely to be malicious\. Attackers try to extract data from your database by embedding malicious SQL code in a web request\. This is known as *SQL injection*\.
+ Strings that appear in the request, for example, values that appear in the `User-Agent` header or text strings that appear in the query string\. You can also use regular expressions \(regex\) to specify these strings\.
Some conditions take multiple values\. For example, you can specify up to 10,000 IP addresses or IP address ranges in an IP condition\.

**Rules**  
You combine conditions into rules to precisely target the requests that you want to allow, block, or count\. AWS WAF provides two types of rules:    
Regular rule  
Regular rules use only conditions to target specific requests\. For example, based on recent requests that you've seen from an attacker, you might create a rule that includes the following conditions:   
+ The requests come from 192\.0\.2\.44\.
+ They contain the value `BadBot` in the `User-Agent` header\.
+ They appear to include SQL\-like code in the query string\.
When a rule includes multiple conditions, as in this example, AWS WAF looks for requests that match all conditions—that is, it `AND`s the conditions together\.   
Add at least one condition to a regular rule\. A regular rule without conditions can't match any requests, so the rule's action \(allow, count, or block\) is never triggered\.   
Rate\-based rule  
Rate\-based rules are like regular rules with an added rate limit\. A rate\-based rule counts the requests that arrive from IP addresses that satisfy the rule's conditions\. If the requests from an IP address exceed the rate limit in a five\-minute period, the rule can trigger an action\.   
Conditions are optional for rate\-based rules\. If you don't add any conditions in a rate\-based rule, the rate limit applies to all IP addresses\. If you combine conditions with the rate limit, the rate limit applies to IP addresses that match the conditions\.   
For example, based on recent requests that you've seen from an attacker, you might create a rate\-based rule that includes the following conditions:   
+ The requests come from 192\.0\.2\.44\.
+ They contain the value `BadBot` in the `User-Agent` header\.
In this rate\-based rule, you also define a rate limit\. In this example, let's say that you create a rate limit of 1,000\. Requests that meet both of the preceding conditions and exceed 1,000 requests per five minutes trigger the rule's action \(block or count\), which is defined in the web ACL\.  
Requests that don't meet both conditions aren't counted towards the rate limit and aren't affected by this rule\.  
As a second example, suppose that you want to limit requests to a particular page on your website\. To do this, you could add the following string match condition to a rate\-based rule:  
+ The **Part of the request to filter on** is `URI`\.
+ The **Match Type** is `Starts with`\. 
+ A **Value to match** is `login`\. 
Further, you specify a `RateLimit` of 1,000\.  
By adding this rate\-based rule to a web ACL, you could limit requests to your login page without affecting the rest of your site\.

**Web ACLs**  
After you combine your conditions into rules, you combine the rules into a web ACL\. This is where you define an action for each rule—allow, block, or count—and a default action:    
**An action for each rule**  
When a web request matches all the conditions in a rule, AWS WAF can either block the request or allow the request to be forwarded to the API Gateway API, CloudFront distribution or an Application Load Balancer\. You specify the action that you want AWS WAF to perform for each rule\.  
AWS WAF compares a request with the rules in a web ACL in the order in which you listed the rules\. AWS WAF then takes the action that is associated with the first rule that the request matches\. For example, if a web request matches one rule that allows requests and another rule that blocks requests, AWS WAF will either allow or block the request depending on which rule is listed first\.  
If you want to test a new rule before you start using it, you also can configure AWS WAF to count the requests that meet all the conditions in the rule\. As with rules that allow or block requests, a rule that counts requests is affected by its position in the list of rules in the web ACL\. For example, if a web request matches a rule that allows requests and another rule that counts requests, and if the rule that allows requests is listed first, the request isn't counted\.   
**A default action**  
The default action determines whether AWS WAF allows or blocks a request that doesn't match all the conditions in any of the rules in the web ACL\. For example, suppose you create a web ACL and add only the rule that you defined before:  
+ The requests come from 192\.0\.2\.44\.
+ They contain the value `BadBot` in the `User-Agent` header\.
+ They appear to include malicious SQL code in the query string\.
If a request doesn't meet all three conditions in the rule and if the default action is `ALLOW`, AWS WAF forwards the request to API Gateway, CloudFront or an Application Load Balancer, and the service responds with the requested object\.  
If you add two or more rules to a web ACL, AWS WAF performs the default action only if a request doesn't satisfy all the conditions in any of the rules\. For example, suppose you add a second rule that contains one condition:  
+ Requests that contain the value `BIGBadBot` in the `User-Agent` header\.
AWS WAF performs the default action only when a request doesn't meet all three conditions in the first rule and doesn't meet the one condition in the second rule\.
On some occasions, AWS WAF might encounter an internal error that delays the response to API Gateway, CloudFront or an Application Load Balancer about whether to allow or block a request\. On those occasions CloudFront will typically allow the request or serve the content\. API Gateway and an Application Load Balancer typically will deny the request and not serve the content\.  
The following illustration shows how AWS WAF checks the rules and performs the actions based on those rules\.

![\[Web ACL\]](http://docs.aws.amazon.com/waf/latest/developerguide/images/web-acl-3a.png)