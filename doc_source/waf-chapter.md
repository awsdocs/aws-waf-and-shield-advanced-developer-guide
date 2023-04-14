# AWS WAF<a name="waf-chapter"></a>

AWS WAF is a web application firewall that lets you monitor the HTTP\(S\) requests that are forwarded to your protected web application resources\. You can protect the following resource types: 
+ Amazon CloudFront distribution
+ Amazon API Gateway REST API
+ Application Load Balancer
+ AWS AppSync GraphQL API
+ Amazon Cognito user pool
+ AWS App Runner service

AWS WAF lets you control access to your content\. Based on criteria that you specify, such as the IP addresses that requests originate from or the values of query strings, the service associated with your protected resource responds to requests either with the requested content, with an HTTP 403 status code \(Forbidden\), or with a custom response\. 

**Note**  
You can also use AWS WAF to protect your applications that are hosted in Amazon Elastic Container Service \(Amazon ECS\) containers\. Amazon ECS is a highly scalable, fast container management service that makes it easy to run, stop, and manage Docker containers on a cluster\. To use this option, you configure Amazon ECS to use an Application Load Balancer that is enabled for AWS WAF to route and protect HTTP\(S\) layer 7 traffic across the tasks in your service\. For more information, see [Service Load Balancing](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/service-load-balancing.html) in the *Amazon Elastic Container Service Developer Guide*\.

**Topics**
+ [How AWS WAF works](how-aws-waf-works.md)
+ [Getting started with AWS WAF](getting-started.md)
+ [Web access control lists \(web ACLs\)](web-acl.md)
+ [Rule groups](waf-rule-groups.md)
+ [Rules](waf-rules.md)
+ [Handling oversize web request components](waf-oversize-request-components.md)
+ [IP sets and regex pattern sets](waf-referenced-set-managing.md)
+ [Customized web requests and responses in AWS WAF](waf-custom-request-response.md)
+ [Labels on web requests](waf-labels.md)
+ [AWS WAF intelligent threat mitigation](waf-managed-protections.md)
+ [Logging web ACL traffic](logging.md)
+ [Listing IP addresses that are being rate limited by rate\-based rules](listing-managed-ips.md)
+ [Testing and tuning your AWS WAF protections](web-acl-testing.md)
+ [How AWS WAF works with Amazon CloudFront features](cloudfront-features.md)
+ [Security in your use of the AWS WAF service](security.md)
+ [AWS WAF quotas](limits.md)
+ [Migrating your AWS WAF Classic resources to AWS WAF](waf-migrating-from-classic.md)