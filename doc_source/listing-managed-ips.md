# Listing IP addresses blocked by rate\-based rules<a name="listing-managed-ips"></a>

You can access the list of IP addresses that are currently blocked by a rate\-based rule by using the CLI, the API, or any of the SDKs\. This topic covers access using the CLI and APIs\. The console doesn't provide this functionality at this time\. 

For the AWS WAF API, the command is [GetRateBasedStatementManagedKeys](https://docs.aws.amazon.com/waf/latest/APIReference/API_GetRateBasedStatementManagedKeys.html)\.

For the AWS WAF CLI, the command is [get\-rate\-based\-statement\-managed\-keys](https://docs.aws.amazon.com/cli/latest/reference/wafv2/get-rate-based-statement-managed-keys.html)\. 

The maximum number of IP addresses that can be blocked for a single rate\-based rule instance is 10,000\. If more than 10,000 addresses exceed the rate limit, AWS WAF blocks those with the highest rates\.

The following shows the syntax for retrieving the list of blocked IP addresses for a rate\-based rule that's being used in a web ACL on an Amazon CloudFront distribution\.

```
aws wafv2 get-rate-based-statement-managed-keys --scope=CLOUDFRONT --region=us-east-1 --web-acl-name=WebACLName --web-acl-id=WebACLId --rule-name=RuleName
```

The following shows the syntax for a regional application, an Amazon API Gateway REST API, an Application Load Balancer, an AWS AppSync GraphQL API, or an Amazon Cognito user pool\. 

```
aws wafv2 get-rate-based-statement-managed-keys --scope=REGIONAL --region=region --web-acl-name=WebACLName --web-acl-id=WebACLId --rule-name=RuleName
```

AWS WAF monitors web requests and manages keys independently for each unique combination of web ACL, optional rule group, and rate\-based rule\. For example, if you define a rate\-based rule inside a rule group, and then use the rule group in a web ACL, AWS WAF monitors web requests and manages keys for that web ACL, rule group reference statement, and rate\-based rule instance\. If you use the same rule group in a second web ACL, AWS WAF monitors web requests and manages keys for this second usage completely independent of your first\.

For a rate\-based rule that you've defined inside a rule group, you need to provide the name of the rule group reference statement in your request, in addition to the web ACL name and the name of the rate\-based rule name inside the rule group\. The following shows the syntax for a regional application where the rate\-based rule is defined inside a rule group, and the rule group is used in a web ACL\. 

```
aws wafv2 get-rate-based-statement-managed-keys --scope=REGIONAL --region=region --web-acl-name=WebACLName --web-acl-id=WebACLId --rule-group-rule-name=RuleGroupRuleName --rule-name=RuleName
```