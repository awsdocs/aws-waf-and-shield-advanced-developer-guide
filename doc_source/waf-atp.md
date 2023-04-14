# AWS WAF Fraud Control account takeover prevention \(ATP\)<a name="waf-atp"></a>

Account takeover is an online illegal activity in which an attacker gains unauthorized access to a person's account\. The attacker might do this in a number of ways, such as using stolen credentials or guessing the victim's password through a series of attempts\. When the attacker gains access, they might steal money, information, or services from the victim\. The attacker might pose as the victim to gain access to other accounts that the victim owns, or to gain access to the accounts of other people or organizations\. Additionally, they might attempt to change the user's password in order to block the victim from their own accounts\. 

You can monitor and control account takeover attempts by implementing the AWS WAF Fraud Control account takeover prevention \(ATP\) feature\. AWS WAF offers this feature in the AWS Managed Rules rule group `AWSManagedRulesATPRuleSet` and companion application integration SDKs\. 

The ATP managed rule group labels and manages requests that might be part of malicious account takeover attempts\. The rule group does this by inspecting login attempts that clients send to your application's login endpoint\. 
+ **Request inspection** – ATP gives you visibility and control over anomalous login attempts and login attempts that use stolen credentials, to prevent account takeovers that might lead to fraudulent activity\. ATP checks email and password combinations against its stolen credential database, which is updated regularly as new leaked credentials are found on the dark web\. ATP aggregates data by IP address and client session, to detect and block clients that send too many requests of a suspicious nature\. 
+ **Response inspection** – For CloudFront distributions, in addition to inspecting incoming login requests, the ATP rule group inspects your application's responses to login attempts, to track success and failure rates\. Using this information, ATP can temporarily block client sessions or IP addresses that have too many login failures\. AWS WAF performs response inspection asynchronously, so this doesn't increase latency in your web traffic\. 

**Note**  
You are charged additional fees when you use this managed rule group\. For more information, see [AWS WAF Pricing](http://aws.amazon.com/waf/pricing/)\.

**Note**  
The ATP feature is not available for Amazon Cognito user pools\.

**Topics**
+ [ATP components](waf-atp-components.md)
+ [Why you should use the application integration SDKs with ATP](waf-atp-with-tokens.md)
+ [Adding the ATP managed rule group to your web ACL](waf-atp-rg-using.md)
+ [Testing and deploying ATP](waf-atp-deploying.md)
+ [AWS WAF Fraud Control account takeover prevention \(ATP\) examples](waf-atp-control-examples.md)