# Resources that you can protect with AWS WAF<a name="how-aws-waf-works-resources"></a>

You can use an AWS WAF web ACL to protect global or regional resource types\. You do this by associating the web ACL with the resources that you want to protect\. The web ACL and any AWS WAF resources that it uses must be located in the Region where the associated resource is located\. For Amazon CloudFront distributions, this is set to US East \(N\. Virginia\)\.

**Amazon CloudFront distributions**  
You can associate an AWS WAF web ACL with a CloudFront distribution using the AWS WAF console or APIs\. You can also associate a web ACL with a CloudFront distribution when you create or update the distribution itself\. To configure an association in AWS CloudFormation, you must use the CloudFront distribution configuration\. For information about Amazon CloudFront, see [Using AWS WAF to Control Access to Your Content](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-awswaf.html) in the *Amazon CloudFront Developer Guide*\.

AWS WAF is available globally for CloudFront distributions, but you must use the Region US East \(N\. Virginia\) to create your web ACL and any resources used in the web ACL, such as rule groups, IP sets, and regex pattern sets\. Some interfaces offer a region choice of "Global \(CloudFront\)"\. Choosing this is identical to choosing Region US East \(N\. Virginia\) or "us\-east\-1"\.

**Regional resources**  
You can protect regional resources in all Regions where AWS WAF is available\. You can see the list at [AWS WAF endpoints and quotas](https://docs.aws.amazon.com/general/latest/gr/waf.html) in the *Amazon Web Services General Reference*\. 

You can use AWS WAF to protect the following regional resource types: 
+ Amazon API Gateway REST API
+ Application Load Balancer
+ AWS AppSync GraphQL API
+ Amazon Cognito user pool
+ AWS App Runner service

You can only associate a web ACL to an Application Load Balancer that's within AWS Regions\. For example, you cannot associate a web ACL to an Application Load Balancer that's on AWS Outposts\.

The web ACL and any other AWS WAF resources that it uses must be located in the same Region as the protected resources\. When monitoring and managing web requests for a protected regional resource, AWS WAF keeps all data in the same Region as the protected resource\. 

**Restrictions on multiple resource associations**  
You can associate a single web ACL with one or more AWS resources, with the following restrictions:
+ You can associate each AWS resource with only one web ACL\. The relationship between web ACL and AWS resources is one\-to\-many\. 
+ You can associate a web ACL with one or more CloudFront distributions\. You cannot associate a web ACL that you have associated with a CloudFront distribution with any other AWS resource type\.