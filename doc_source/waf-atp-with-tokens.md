# Why you should use the application integration SDKs with ATP<a name="waf-atp-with-tokens"></a>

The ATP managed rule group requires the challenge tokens that the application integration SDKs generate\. The tokens enable the full set of protections that the rule group offers\. 

We highly recommend implementing the application integration SDKs, for the most effective use of the ATP rule group\. The challenge script must run before the ATP rule group in order for the rule group to benefit from the tokens that the script acquires\. This happens automatically with the application integration SDKs\. If you are unable to use the SDKs, you can alternately configure your web ACL so that it runs the Challenge or CAPTCHA rule action against all requests that will be inspected by the ATP rule group\. Using the Challenge or CAPTCHA rule action can incur additional fees\. For pricing details, see [AWS WAF Pricing](http://aws.amazon.com/waf/pricing/)\. 

**Capabilities of the ATP rule group that don't require a token**  
When web requests don't have a token, the ATP managed rule group is capable of blocking the following types of traffic:
+ Single IP addresses that make a lot of login requests\. 
+ Single IP addresses that make a lot of failed login requests in a short amount of time\. 
+ Login attempts with password traversal, using the same username but changing passwords\. 

**Capabilities of the ATP rule group that require a token**  
The information provided in the challenge token expands the capabilities of the rule group and of your overall client application security\. 

The token provides client information with each web request that enables the ATP rule group to separate legitimate client sessions from ill\-behaved client sessions, even when both originate from a single IP address\. The rule group uses information in the tokens to aggregate client session request behavior for fine\-tuned detection and mitigation\. 

When the token is available in web requests, the ATP rule group can detect and block the following additional categories of clients at the session level: 
+ Client sessions that fail the silent challenge that the SDKs manage\. 
+ Client sessions that traverse usernames or passwords\. This is also known as credential stuffing\.
+ Client sessions that repeatedly use stolen credentials to log in\.
+ Client sessions that spend a long time trying to log in\. 
+ Clients sessions that make a lot of login requests\. The ATP rule group provides better client isolation than the AWS WAF rate\-based rule, which blocks clients by IP address\. The ATP rule group also uses a lower threshold\. 
+ Clients sessions that make a lot of failed login requests in a short amount of time\. This functionality is available for protected Amazon CloudFront distributions\.

For more information about the rule group capabilities see [AWS WAF Fraud Control account takeover prevention \(ATP\) rule group](aws-managed-rule-groups-atp.md)\.

For information about the SDKs, see [AWS WAF client application integration](waf-application-integration.md)\. For information about AWS WAF tokens, see [AWS WAF web request tokens](waf-tokens.md)\. For information about the rule actions, see [CAPTCHA and Challenge actions in AWS WAF](waf-captcha-and-challenge.md)\.