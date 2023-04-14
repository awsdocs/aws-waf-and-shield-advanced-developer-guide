# Listing IP addresses that are being rate limited by rate\-based rules<a name="listing-managed-ips"></a>

A rate\-based rule applies its rule action to requests from IP addresses that are in the rule's managed keys list and that match the rule's scope\-down statement\. When a rule has no scope\-down statement, it applies the action to all requests from the IP addresses that are in the list\. The rule applies its rule action to rate limit the matching requests\. The action is usually Block but it can be any valid rule action except for Allow\. The maximum number of IP addresses that can be rate limited by a single rate\-based rule instance is 10,000\. If more than 10,000 addresses exceed the rate limit, AWS WAF limits those with the highest rates\. For more information about rate\-based rules, see [Rate\-based rule statement](waf-rule-statement-type-rate-based.md)\. 

You can access the list of IP addresses that are currently being rate limited by a rate\-based rule by using the CLI, the API, or any of the SDKs\. This topic covers access using the CLI and APIs\. The console doesn't provide this functionality at this time\. 

For the AWS WAF API, the command is [GetRateBasedStatementManagedKeys](https://docs.aws.amazon.com/waf/latest/APIReference/API_GetRateBasedStatementManagedKeys.html)\.

For the AWS WAF CLI, the command is [get\-rate\-based\-statement\-managed\-keys](https://docs.aws.amazon.com/cli/latest/reference/wafv2/get-rate-based-statement-managed-keys.html)\. 

The following shows the syntax for retrieving the list of rate limited IP addresses for a rate\-based rule that's being used in a web ACL on an Amazon CloudFront distribution\.

```
aws wafv2 get-rate-based-statement-managed-keys --scope=CLOUDFRONT --region=us-east-1 --web-acl-name=WebACLName --web-acl-id=WebACLId --rule-name=RuleName
```

The following shows the syntax for a regional application, an Amazon API Gateway REST API, an Application Load Balancer, an AWS AppSync GraphQL API, Amazon Cognito user pool, or an AWS App Runner service\. 

```
aws wafv2 get-rate-based-statement-managed-keys --scope=REGIONAL --region=region --web-acl-name=WebACLName --web-acl-id=WebACLId --rule-name=RuleName
```

AWS WAF monitors web requests and manages keys independently for each unique combination of web ACL, optional rule group, and rate\-based rule\. For example, if you define a rate\-based rule inside a rule group, and then use the rule group in a web ACL, AWS WAF monitors web requests and manages keys for that web ACL, rule group reference statement, and rate\-based rule instance\. If you use the same rule group in a second web ACL, AWS WAF monitors web requests and manages keys for this second usage completely independent of your first\.

For a rate\-based rule that you've defined inside a rule group, you need to provide the name of the rule group reference statement in your request, in addition to the web ACL name and the name of the rate\-based rule inside the rule group\. The following shows the syntax for a regional application where the rate\-based rule is defined inside a rule group, and the rule group is used in a web ACL\. 

```
aws wafv2 get-rate-based-statement-managed-keys --scope=REGIONAL --region=region --web-acl-name=WebACLName --web-acl-id=WebACLId --rule-group-rule-name=RuleGroupRuleName --rule-name=RuleName
```