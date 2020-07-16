# Listing IP addresses blocked by rate\-based rules<a name="listing-managed-ips"></a>

You can access the list of IP addresses that are currently blocked by a rate\-based rule by using the CLI, the API, or any of the SDKs\. This topic covers access using the CLI and APIs\. The console doesn't provide this functionality at this time\. 

For the AWS WAF API, the command is [GetRateBasedStatementManagedKeys](https://docs.aws.amazon.com/waf/latest/APIReference/API_GetRateBasedStatementManagedKeys.html)\.

For the AWS WAF CLI, the command is [get\-rate\-based\-statement\-managed\-keys](https://docs.aws.amazon.com/cli/latest/reference/wafv2/get-rate-based-statement-managed-keys.html)\. 

The following shows the syntax for retrieving the list of blocked IP addresses for a rate\-based rule that's being used on an Amazon CloudFront distribution\.

```
aws wafv2 get-rate-based-statement-managed-keys --scope=CLOUDFRONT --region=us-east-1 --web-acl-name=WebACLName --web-acl-id=WebACLId --rule-name=RuleName
```

The following shows the syntax for a regional application, an Amazon API Gateway REST API or an Application Load Balancer\. 

```
aws wafv2 get-rate-based-statement-managed-keys --scope=REGIONAL --region=region --web-acl-name=WebACLName --web-acl-id=WebACLId --rule-name=RuleName
```