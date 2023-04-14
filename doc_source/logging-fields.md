# Log Fields<a name="logging-fields"></a>

The following list describes the possible log fields\. 

**action**  
The action that was applied to the request\. Allow and Block are terminating rule actions\. Count is a non\-terminating rule action\. CAPTCHA and Challenge are non\-terminating if the request includes a valid token and terminating if it doesn't\. 

**args**  
The query string\.

**captchaResponse**  
The CAPTCHA response to the request, populated when the CAPTCHA action results in the termination of web request inspection\. The CAPTCHA action terminates web request inspection when the request either doesn't include a token or the token is invalid or expired\. This field includes a response code and a failure reason\.

**challengeResponse**  
The challenge response to the request, populated when the Challenge action results in the termination of web request inspection\. The Challenge action terminates web request inspection when the request either doesn't include a token or the token is invalid or expired\. This field includes a response code and a failure reason\. 

**clientIp**  
The IP address of the client sending the request\.

**country**  
The source country of the request\. If AWS WAF is unable to determine the country of origin, it sets this field to `-`\. 

**excludedRules**  
Used only for rule group rules\. The list of rules in the rule group that you have excluded\. The action for these rules is set to Count\.   
If you override a rule to count using the override rule action option, matches aren't listed here\. They're listed as the action pairs `action` and `overriddenAction`\.    
exclusionType  
A type that indicates that the excluded rule has the action Count\.  
ruleId  
The ID of the rule within the rule group that is excluded\.

**formatVersion**  
The format version for the log\.

**headers**  
The list of headers\.

**httpMethod**  
The HTTP method in the request\.

**httpRequest**  
The metadata about the request\.

**httpSourceId**  
The ID of the associated resource:   
+ For an Amazon CloudFront distribution, the ID is the `distribution-id` in the ARN syntax: 

  `arn:partitioncloudfront::account-id:distribution/distribution-id` 
+ For an Application Load Balancer, the ID is the `load-balancer-id` in the ARN syntax: 

  `arn:partition:elasticloadbalancing:region:account-id:loadbalancer/app/load-balancer-name/load-balancer-id`
+ For an Amazon API Gateway REST API, the ID is the `api-id` in the ARN syntax: 

  `arn:partition:apigateway:region::/restapis/api-id/stages/stage-name`
+ For an AWS AppSync GraphQL API, the ID is the `GraphQLApiId` in the ARN syntax: 

  `arn:partition:appsync:region:account-id:apis/GraphQLApiId`
+ For an Amazon Cognito user pool, the ID is the `user-pool-id` in the ARN syntax: 

  `arn:partition:cognito-idp:region:account-id:userpool/user-pool-id`
+ For an AWS App Runner service, the ID is the `apprunner-service-id` in the ARN syntax: 

  `arn:partition:apprunner:region:account-id:service/apprunner-service-name/apprunner-service-id`

**httpSourceName**  
The source of the request\. Possible values: `CF` for Amazon CloudFront, `APIGW` for Amazon API Gateway, `ALB` for Application Load Balancer, `APPSYNC` for AWS AppSync, `COGNITOIDP` for Amazon Cognito, and `APPRUNNER` for App Runner\.

**httpVersion**  
The HTTP version\.

**labels**  
The labels on the web request\. These labels were applied by rules that were used to evaluate the request\. AWS WAF logs the first 100 labels\. 

**limitKey**  
Indicates the IP address source that AWS WAF should use to aggregate requests for rate limiting by a rate\-based rule\. Possible values are `IP`, for web request origin, and `FORWARDED_IP`, for an IP forwarded in a header in the request\.

**limitValue**  
The IP address used by a rate\-based rule to aggregate requests for rate limiting\. If a request contains an IP address that isn't valid, the `limitvalue` is `INVALID`\.

**maxRateAllowed**  
The maximum number of requests, which have an identical value in the field that is specified by `limitKey`, allowed in a five minute period\. If the number of requests exceeds the `maxRateAllowed` and the other predicates specified in the rule are also met, AWS WAF triggers the action that is specified for this rule\.

**nonTerminatingMatchingRules**  
The list of non\-terminating rules that match the request\.     
action  
The action that AWS WAF applied to the request\. This indicates either count, CAPTCHA, or challenge\. The CAPTCHA and Challenge are non\-terminating when the web request contains a valid token\.  
overriddenAction  
Used only for rule group rules that have a rule action override in place in the web ACL\. This is the action that the rule group rule is configured for, and not the action that was applied to the request\. The action that AWS WAF applied is the `action` value\.   
ruleId  
The ID of the rule that matched the request and was non\-terminating\.   
ruleMatchDetails  
Detailed information about the rule that matched the request\. This field is only populated for SQL injection and cross\-site scripting \(XSS\) match rule statements\. A matching rule might require a match for more than one inspection criteria, so these match details are provided as an array of match criteria\. 

**oversizeFields**  
The list of fields in the web request that were inspected by the web ACL and that are over the AWS WAF inspection limit\. If a field is oversize but the web ACL doesn't inspect it, it won't be listed here\.   
This list can contain zero or more of the following values: `REQUEST_BODY`, `REQUEST_JSON_BODY`, `REQUEST_HEADERS`, and `REQUEST_COOKIES`\. For more information about oversize fields, see [Handling oversize web request components](waf-oversize-request-components.md)\.

**rateBasedRuleId**  
The ID of the rate\-based rule that acted on the request\. If this has terminated the request, the ID for `rateBasedRuleId` is the same as the ID for `terminatingRuleId`\.

**rateBasedRuleList**  
The list of rate\-based rules that acted on the request\.

**rateBasedRuleName**  
The name of the rate\-based rule that acted on the request\. 

**requestHeadersInserted**  
The list of headers inserted for custom request handling\.

**requestId**  
The ID of the request, which is generated by the underlying host service\. For Application Load Balancer, this is the trace ID\. For all others, this is the request ID\. 

**responseCodeSent**  
The response code sent with a custom response\.

**ruleGroupId**  
The ID of the rule group\. If the rule blocked the request, the ID for `ruleGroupID` is the same as the ID for `terminatingRuleId`\. 

**ruleGroupList**  
The list of rule groups that acted on this request, with match information\.

**terminatingRule**  
The rule that terminated the request\. If this is a non\-null value, it contains the following additional fields\.     
action  
The action that AWS WAF applied to the request\. This indicates either allow, block, CAPTCHA, or challenge\. The CAPTCHA and Challenge actions are terminating when the web request doesn't contain a valid token\.  
overriddenAction  
Used only for rule group rules that have a rule action override in place in the web ACL\. This is the action that the rule group rule is configured for, and not the action that was applied to the request\. The action that AWS WAF applied is the `action` value\.   
ruleId  
The ID of the rule that matched the request\.   
ruleMatchDetails  
Detailed information about the rule that matched the request\. This field is only populated for SQL injection and cross\-site scripting \(XSS\) match rule statements\. A matching rule might require a match for more than one inspection criteria, so these match details are provided as an array of match criteria\. 

**terminatingRuleId**  
The ID of the rule that terminated the request\. If nothing terminates the request, the value is `Default_Action`\.

**terminatingRuleMatchDetails**  
Detailed information about the terminating rule that matched the request\. A terminating rule has an action that ends the inspection process against a web request\. Possible actions for a terminating rule include Allow, Block, CAPTCHA, and Challenge\. During the inspection of a web request, at the first rule that matches the request and that has a terminating action, AWS WAF stops the inspection and applies the action\. The web request might contain other threats, in addition to the one that's reported in the log for the matching terminating rule\.  
This is only populated for SQL injection and cross\-site scripting \(XSS\) match rule statements\. The matching rule might require a match for more than one inspection criteria, so these match details are provided as an array of match criteria\. 

**terminatingRuleType**  
The type of rule that terminated the request\. Possible values: RATE\_BASED, REGULAR, GROUP, and MANAGED\_RULE\_GROUP\.

**timestamp**  
The timestamp in milliseconds\.

**uri**  
The URI of the request\. 

**webaclId**  
The GUID of the web ACL\.