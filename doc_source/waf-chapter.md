# AWS WAF<a name="waf-chapter"></a>

AWS WAF is a web application firewall that lets you monitor the HTTP\(S\) requests that are forwarded to an Amazon CloudFront distribution, an Amazon API Gateway REST API, or an Application Load Balancer\. 

AWS WAF also lets you control access to your content\. Based on conditions that you specify, such as the IP addresses that requests originate from or the values of query strings, an Amazon CloudFront distribution, an Amazon API Gateway REST API, or an Application Load Balancer responds to requests either with the requested content or with an HTTP 403 status code \(Forbidden\)\. You can also configure CloudFront to return a custom error page when a request is blocked\.

**Note**  
You can also use AWS WAF to protect your applications that are hosted in Amazon Elastic Container Service \(Amazon ECS\) containers\. Amazon ECS is a highly scalable, fast container management service that makes it easy to run, stop, and manage Docker containers on a cluster\. To use this option, you configure Amazon ECS to use an Application Load Balancer that is enabled for AWS WAF to route and protect HTTP\(S\) layer 7 traffic across the tasks in your service\. For more information, see [Service Load Balancing](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/service-load-balancing.html) in the *Amazon Elastic Container Service Developer Guide*\.

**Topics**
+ [How AWS WAF works](how-aws-waf-works.md)
+ [Getting started with AWS WAF](getting-started.md)
+ [Migrating your AWS WAF Classic resources to AWS WAF](waf-migrating-from-classic.md)
+ [Managing and using a Web Access Control List \(Web ACL\)](web-acl.md)
+ [Rule groups](waf-rule-groups.md)
+ [AWS WAF rules](waf-rules.md)
+ [IP sets and regex pattern sets](waf-referenced-set-managing.md)
+ [Logging Web ACL traffic information](logging.md)
+ [Listing IP addresses blocked by rate\-based rules](listing-managed-ips.md)
+ [How AWS WAF works with Amazon CloudFront features](cloudfront-features.md)
+ [Security in AWS WAF](security.md)
+ [AWS WAF quotas](limits.md)