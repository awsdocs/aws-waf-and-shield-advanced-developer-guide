# How AWS WAF works<a name="how-aws-waf-works"></a>

You use AWS WAF to control how an Amazon CloudFront distribution, an Amazon API Gateway REST API, an Application Load Balancer, or an AWS AppSync GraphQL API responds to HTTP\(S\) web requests\. 
+ **Web ACLs** – You use a web access control list \(ACL\) to protect a set of AWS resources\. You create a web ACL and define its protection strategy by adding rules\. Rules define criteria for inspecting web requests and specify how to handle requests that match the criteria\. You set a default action for the web ACL that indicates whether to block or allow through those requests that pass the rules inspections\. 
+ **Rules** – Each rule contains a statement that defines the inspection criteria, and an action to take if a web request meets the criteria\. When a web request meets the criteria, that's a match\. You can configure rules to block matching requests, allow them through, count them, or run CAPTCHA controls against them\. 
+ **Rules groups** – You can use rules individually or in reusable rule groups\. AWS Managed Rules and AWS Marketplace sellers provide managed rule groups for your use\. You can also define your own rule groups\.

After you create your web ACL, you can associate it with one or more AWS resources\. The resource types that you can protect using AWS WAF web ACLs are an Amazon CloudFront distribution, an Amazon API Gateway REST API, an Application Load Balancer, and an AWS AppSync GraphQL API\. 

AWS WAF is available in the Regions listed at [AWS service endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html)\. 
+ For an Amazon API Gateway REST API, an Application Load Balancer, or an AWS AppSync GraphQL API, you can use any of the Regions in the list\. 
+ For a CloudFront distribution, AWS WAF is available globally, but you must use the Region US East \(N\. Virginia\) for all of your work\. You must create your web ACL using the Region US East \(N\. Virginia\)\. You must also use this Region to create any other resources that you use in your web ACL, like rule groups, IP sets, and regex pattern sets\. 

  Some interfaces offer a region choice of "Global \(CloudFront\)"\. Choosing this is identical to choosing Region US East \(N\. Virginia\) or "us\-east\-1"\.

You can associate a web ACL with a CloudFront distribution when you create or update the distribution itself\. For information, see [Using AWS WAF to Control Access to Your Content](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-awswaf.html) in the *Amazon CloudFront Developer Guide*\.

You can only associate a web ACL to an Application Load Balancer within AWS Regions\. For example, you cannot associate a web ACL to an Application Load Balancer that is on AWS Outposts\.

**Restrictions on multiple associations**  
You can associate a single web ACL with one or more AWS resources, according to the following restrictions:
+ You can associate each AWS resource with only one web ACL\. The relationship between web ACL and AWS resources is one\-to\-many\. 
+ You can associate a web ACL with one or more CloudFront distributions\. You cannot associate a web ACL that you have associated with a CloudFront distribution with any other AWS resource type\.

## AWS WAF Web ACL capacity units \(WCU\)<a name="aws-waf-capacity-units"></a>

AWS WAF uses web ACL capacity units \(WCU\) to calculate and control the operating resources that are required to run your rules, rule groups, and web ACLs\. AWS WAF enforces WCU limits when you configure your rule groups and web ACLs\. WCUs don't affect how AWS WAF inspects web traffic\. 

AWS WAF calculates capacity differently for each rule type, to reflect each rule's relative cost\. Simple rules that cost little to run use fewer WCUs than more complex rules that use more processing power\. For example, a size constraint rule statement uses fewer WCUs than a statement that inspects against a regex pattern set\. 

AWS WAF manages capacity for rules, rule groups, and web ACLs:
+ **Rule capacity** – AWS WAF calculates rule capacity when you create or update a rule\. For some basic guidelines for rule capacity requirements, see the listings for the various rule statements at [AWS WAF rule statements](waf-rule-statements.md)\. You can also get an idea of the capacity required for the various rule types in the AWS WAF console by creating a web ACL or rule group and adding individual rules to it\. The console displays the capacity units used as you add the rules\. 
+ **Rule group capacity** – AWS WAF requires that each rule group is assigned an immutable capacity at creation\. This is true for managed rule groups and rule groups that you create through AWS WAF\. When you modify a rule group, your changes must keep the rule group's WCU within its capacity\. This ensures that web ACLs that are using the rule group remain within their maximum capacity\. 
+ **Web ACL capacity** – The maximum capacity for a web ACL is 1,500, which is sufficient for most use cases\. If you need more capacity, contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\. 

## AWS WAF pricing<a name="aws-waf-pricing"></a>

With AWS WAF, you pay only for the web ACLs and rule groups that you create, and for the number of HTTP\(S\) requests that AWS WAF inspects\. For more information, see [AWS WAF Pricing](http://aws.amazon.com/waf/pricing/)\. 