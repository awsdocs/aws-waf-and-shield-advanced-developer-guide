# AWS WAF Classic<a name="classic-waf-chapter"></a>

**Note**  
This is **AWS WAF Classic** documentation\. If you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November, 2019, and you have not migrated your web ACLs over yet, you need to use AWS WAF Classic to access those resources\. Otherwise, do not use this version\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

AWS WAF Classic is a web application firewall that lets you monitor the HTTP and HTTPS requests that are forwarded to an Amazon API Gateway API, Amazon CloudFront or an Application Load Balancer\. AWS WAF Classic also lets you control access to your content\. Based on conditions that you specify, such as the IP addresses that requests originate from or the values of query strings, API Gateway, CloudFront or an Application Load Balancer responds to requests either with the requested content or with an HTTP 403 status code \(Forbidden\)\. You also can configure CloudFront to return a custom error page when a request is blocked\.

**Topics**
+ [Setting Up AWS WAF Classic](classic-setting-up-waf.md)
+ [How AWS WAF Classic Works](classic-how-aws-waf-works.md)
+ [AWS WAF Classic Pricing](classic-aws-waf-pricing.md)
+ [Getting Started with AWS WAF Classic](classic-getting-started.md)
+ [Tutorials for AWS WAF Classic](classic-tutorials.md)
+ [Creating and Configuring a Web Access Control List \(Web ACL\)](classic-web-acl.md)
+ [Logging Web ACL Traffic Information](classic-logging.md)
+ [Listing IP addresses blocked by rate\-based rules](classic-listing-managed-ips.md)
+ [How AWS WAF Classic Works with Amazon CloudFront Features](classic-cloudfront-features.md)
+ [Security in AWS WAF Classic](classic-security.md)
+ [AWS WAF Classic Limits](classic-limits.md)