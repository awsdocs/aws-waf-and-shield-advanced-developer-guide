# AWS WAF Fraud Control account takeover prevention \(ATP\) rule group<a name="aws-managed-rule-groups-atp"></a>

VendorName: `AWS`, Name: `AWSManagedRulesATPRuleSet`, WCU: 50

The AWS WAF Fraud Control account takeover prevention \(ATP\) managed rule group labels and manages requests that might be part of malicious account takeover attempts\. The rule group does this by inspecting login attempts that clients send to your application's login endpoint\. 
+ **Request inspection** – ATP gives you visibility and control over anomalous login attempts and login attempts that use stolen credentials, to prevent account takeovers that might lead to fraudulent activity\. ATP checks email and password combinations against its stolen credential database, which is updated regularly as new leaked credentials are found on the dark web\. ATP aggregates data by IP address and client session, to detect and block clients that send too many requests of a suspicious nature\. 
+ **Response inspection** – For CloudFront distributions, in addition to inspecting incoming login requests, the ATP rule group inspects your application's responses to login attempts, to track success and failure rates\. Using this information, ATP can temporarily block client sessions or IP addresses that have too many login failures\. AWS WAF performs response inspection asynchronously, so this doesn't increase latency in your web traffic\. 

**Using this rule group**  
This rule group requires specific configuration\. To configure and implement this rule group, see the guidance at [AWS WAF Fraud Control account takeover prevention \(ATP\)](waf-atp.md)\. 

This rule group is part of the intelligent threat mitigation protections in AWS WAF\. For information, see [AWS WAF intelligent threat mitigation](waf-managed-protections.md)\.

**Note**  
You are charged additional fees when you use this managed rule group\. For more information, see [AWS WAF Pricing](http://aws.amazon.com/waf/pricing/)\.

To keep your costs down and to be sure you're managing your web traffic as you want, use this rule group in accordance with the guidance at [Best practices for intelligent threat mitigation](waf-managed-protections-best-practices.md)\.

This rule group isn't available for use with Amazon Cognito user pools\. You can't associate a web ACL that uses this rule group with a user pool, and you can't add this rule group to a web ACL that's already associated with a user pool\.

This rule group doesn't provide versioning or SNS update notifications\. 

**Token labels**  
This rule group uses AWS WAF token management to inspect and label web requests according to the status of their AWS WAF tokens\. AWS WAF uses tokens for client session tracking and verification\. 

AWS WAF applies one of the following labels when it inspects a web request's token and challenge timestamp\. AWS WAF doesn't add labeling about the status of the CAPTCHA timestamp\. 
+ `awswaf:managed:token:accepted` – The request token is present and has an unexpired challenge timestamp\. 
+ `awswaf:managed:token:rejected` – The request token is present but is either corrupt or has an expired challenge timestamp\.
+ `awswaf:managed:token:absent` – The request doesn't have a token\.

For more information, see [AWS WAF web request tokens](waf-tokens.md)\.

**ATP labels**  
The ATP managed rule group generates labels with the namespace prefix `awswaf:managed:aws:atp:` followed by the custom namespace\. 

## Account takeover prevention rules listing<a name="aws-managed-rule-groups-atp-rules"></a>

The following table lists the ATP rules in `AWSManagedRulesATPRuleSet` and the labels that the rule group adds to web requests\.


| Rule name | Description and label | 
| --- | --- | 
| UnsupportedCognitoIDP | Inspects for web traffic going to an Amazon Cognito user pool\. ATP isn't available for use with Amazon Cognito user pools, and this rule helps to ensure that the other ATP rule group rules are not used to evaluate user pool traffic\. Rule action: Block Label: `awswaf:managed:aws:atp:unsupported:cognito_idp`  | 
| VolumetricIpHigh | Inspects for high volumes of requests sent from individual IP addresses\. A high volume is more than 20 requests in a 10 minute window\.   The thresholds that this rule applies can vary slightly due to latency\. For the high volume, a few requests might make it through beyond the limit before the rule action is applied\.   Rule action: Block Label: `awswaf:managed:aws:atp:aggregate:volumetric:ip:high` The rule group applies the following labels to requests with medium volumes \(16\-20 requests per 10 minute window\) and low volumes \(11\-15 requests per 10 minute window\), but takes no action on them: `awswaf:managed:aws:atp:aggregate:volumetric:ip:medium` and `awswaf:managed:aws:atp:aggregate:volumetric:ip:low`\. | 
| VolumetricSession |  Inspects for high volumes of requests sent from individual client sessions\.  This inspection only applies when the web request has a token\. Tokens are added to requests by the application integration SDKs and by the rule actions CAPTCHA and Challenge\. For more information, see [AWS WAF web request tokens](waf-tokens.md)\.  The thresholds that this rule applies can vary slightly due to latency\. A few requests might make it through beyond the limit before the rule action is applied\.   Rule action: Block Label: `awswaf:managed:aws:atp:aggregate:volumetric:session`  | 
| AttributeCompromisedCredentials |  Inspects for multiple requests from the same client session that use stolen credentials\.  Rule action: Block Label: `awswaf:managed:aws:atp:aggregate:attribute:compromised_credentials`  | 
| AttributeUsernameTraversal |  Inspects for multiple requests from the same client session that use username traversal\.  Rule action: Block Label: `awswaf:managed:aws:atp:aggregate:attribute:username_traversal`  | 
| AttributePasswordTraversal |  Inspects for multiple requests from the same client session that use password traversal\.  Rule action: Block Label: `awswaf:managed:aws:atp:aggregate:attribute:password_traversal`  | 
| AttributeLongSession |  Inspects for multiple requests from the same client session that use long lasting sessions\.  This inspection only applies when the web request has a token\. Tokens are added to requests by the application integration SDKs and by the rule actions CAPTCHA and Challenge\. For more information, see [AWS WAF web request tokens](waf-tokens.md)\. Rule action: Block Label: `awswaf:managed:aws:atp:aggregate:attribute:long_session`  | 
| TokenRejected |  Inspects for requests with tokens that are rejected by AWS WAF token management\.  This inspection only applies when the web request has a token\. Tokens are added to requests by the application integration SDKs and by the rule actions CAPTCHA and Challenge\. For more information, see [AWS WAF web request tokens](waf-tokens.md)\. Rule action: Block Label: None\. To check for token rejected, use a label match rule to match on the label: `awswaf:managed:token:rejected`  | 
| SignalMissingCredential |  Inspects for requests with credentials that are missing the username or password\.  Rule action: Block Label: `awswaf:managed:aws:atp:signal:missing_credential`  | 
| No rule\. For each matching request, the rule group adds the label and takes no action on the request\. |  Searches the stolen credential database for the credentials that were submitted in the request\.  Rule action: no action Label: `awswaf:managed:aws:atp:signal:credential_compromised`  | 
| No rule\. For each matching request, the rule group adds the label and takes no action on the request\. |  Inspects for multiple requests from the same client session that use a suspicious TLS fingerprint\.   Available only for protected Amazon CloudFront distributions\.   Rule action: no action Label: `awswaf:managed:aws:atp:aggregate:attribute:suspicious_tls_fingerprint`  | 
| VolumetricIpFailedLoginResponseHigh |  Inspects for IP addresses that have recently been the source of too high a rate of failed login attempts\. If you've configured the rule group to inspect the response body or JSON components, AWS WAF can inspect the first 65,536 bytes \(64 KB\) of these component types for success or failure indicators\.  This rule applies the rule action and labeling to new web requests from an IP address, based on the success and failure responses from the protected resource to recent login attempts from the same IP address\. You define how to count successes and failures when you configure the rule group\.   AWS WAF only evaluates this rule in web ACLs that protect Amazon CloudFront distributions\.   The thresholds that this rule applies can vary slightly due to latency\. It's possible for the client to send more failed login attempts than are allowed before the rule starts matching on subsequent attempts\.   Rule action: Block Label: `awswaf:managed:aws:atp:aggregate:volumetric:ip:failed_login_response:high`  | 
| VolumetricSessionFailedLoginResponseHigh |  Inspects for client sessions that have recently been the source of too high a rate of failed login attempts\. If you've configured the rule group to inspect the response body or JSON components, AWS WAF can inspect the first 65,536 bytes \(64 KB\) of these component types for success or failure indicators\.  This rule applies the rule action and labeling to new web requests from a client session, based on the success and failure responses from the protected resource to recent login attempts from the same client session\. You define how to count successes and failures when you configure the rule group\.   AWS WAF only evaluates this rule in web ACLs that protect Amazon CloudFront distributions\.   The thresholds that this rule applies can vary slightly due to latency\. It's possible for the client to send more failed login attempts than are allowed before the rule starts matching on subsequent attempts\.   This inspection only applies when the web request has a token\. Tokens are added to requests by the application integration SDKs and by the rule actions CAPTCHA and Challenge\. For more information, see [AWS WAF web request tokens](waf-tokens.md)\. Rule action: Block Label: `awswaf:managed:aws:atp:aggregate:volumetric:session:failed_login_response:high`  | 