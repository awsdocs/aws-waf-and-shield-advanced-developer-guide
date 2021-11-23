# What are AWS WAF, AWS Shield, and AWS Firewall Manager?<a name="what-is-aws-waf"></a>

AWS WAF is a web application firewall that lets you monitor the HTTP and HTTPS requests that are forwarded to an Amazon CloudFront distribution, an Amazon API Gateway REST API, an Application Load Balancer, or an AWS AppSync GraphQL API\. AWS WAF also lets you control access to your content\. Based on conditions that you specify, such as the IP addresses that requests originate from or the values of query strings, Amazon CloudFront, Amazon API Gateway, Application Load Balancer, or AWS AppSync responds to requests either with the requested content or with an HTTP 403 status code \(Forbidden\)\. You also can configure CloudFront to return a custom error page when a request is blocked\.

At the simplest level, AWS WAF lets you choose one of the following behaviors:
+ **Allow all requests except the ones that you specify** – This is useful when you want Amazon CloudFront, Amazon API Gateway, Application Load Balancer, or AWS AppSync to serve content for a public website, but you also want to block requests from attackers\.
+ **Block all requests except the ones that you specify** – This is useful when you want to serve content for a restricted website whose users are readily identifiable by properties in web requests, such as the IP addresses that they use to browse to the website\. 
+ **Count requests that match your criteria** – You can use the count action to track your web traffic without modifying how you handle it\. You can use this for general monitoring and also to test your new web request handling rules\. When you want to allow or block requests based on new properties in the web requests, you can first configure AWS WAF to count the requests that match those properties\. This lets you confirm your new configuration settings before you implement new allow or block actions\.
+ **Run CAPTCHA checks against requests that match your criteria** – You can implement CAPTCHA controls against requests to help reduce bot traffic to your protected resources\.

Using AWS WAF has several benefits:
+ Additional protection against web attacks using conditions that you specify\. You can define conditions by using characteristics of web requests such as the following:
  + IP addresses that requests originate from\.
  + Country that requests originate from\.
  + Values in request headers\.
  + Strings that appear in requests, either specific strings or strings that match regular expression \(regex\) patterns\.
  + Length of requests\.
  + Presence of SQL code that is likely to be malicious \(known as *SQL injection*\)\.
  + Presence of a script that is likely to be malicious \(known as *cross\-site scripting*\)\.
+ Rules that can allow, block, or count web requests that meet the specified conditions\. Alternatively, rules can block or count web requests that not only meet the specified conditions, but also exceed a specified number of requests in any 5\-minute period\. 
+ Rules that you can reuse for multiple web applications\.
+ Managed rule groups from AWS and AWS Marketplace sellers\.
+ Real\-time metrics and sampled web requests\.
+ Automated administration using the AWS WAF API\.

## AWS Shield<a name="ddos-intro"></a>

You can use AWS WAF web access control lists \(web ACLs\) to help minimize the effects of a distributed denial of service \(DDoS\) attack\. For additional protection against DDoS attacks, AWS also provides AWS Shield Standard and AWS Shield Advanced\. AWS Shield Standard is automatically included at no extra cost beyond what you already pay for AWS WAF and your other AWS services\. AWS Shield Advanced provides expanded DDoS attack protection for your Amazon EC2 instances, Elastic Load Balancing load balancers, CloudFront distributions, Route 53 hosted zones, and AWS Global Accelerator accelerators\. AWS Shield Advanced incurs additional charges\. 

For more information about AWS Shield Standard and AWS Shield Advanced, see [AWS Shield](shield-chapter.md)\.

## AWS Firewall Manager<a name="fms-intro"></a>

AWS Firewall Manager simplifies your administration and maintenance tasks across multiple accounts and resources for a variety of protections, including AWS WAF, AWS Shield Advanced, Amazon VPC security groups, AWS Network Firewall, and Amazon Route 53 Resolver DNS Firewall\. With Firewall Manager, you set up your protections just once and the service automatically applies them across your accounts and resources, even as you add new accounts and resources\. 

For more information about Firewall Manager, see [AWS Firewall Manager](fms-chapter.md)\.