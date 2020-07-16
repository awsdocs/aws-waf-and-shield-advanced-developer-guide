# What are AWS WAF, AWS Shield, and AWS Firewall Manager?<a name="what-is-aws-waf"></a>

AWS WAF is a web application firewall that lets you monitor the HTTP and HTTPS requests that are forwarded to an Amazon CloudFront distribution, an Amazon API Gateway REST API, or an Application Load Balancer\. AWS WAF also lets you control access to your content\. Based on conditions that you specify, such as the IP addresses that requests originate from or the values of query strings, API Gateway, CloudFront or an Application Load Balancer responds to requests either with the requested content or with an HTTP 403 status code \(Forbidden\)\. You also can configure CloudFront to return a custom error page when a request is blocked\.

At the simplest level, AWS WAF lets you choose one of the following behaviors:
+ **Allow all requests except the ones that you specify** – This is useful when you want CloudFront or an Application Load Balancer to serve content for a public website, but you also want to block requests from attackers\.
+ **Block all requests except the ones that you specify** – This is useful when you want to serve content for a restricted website whose users are readily identifiable by properties in web requests, such as the IP addresses that they use to browse to the website\. 
+ **Count the requests that match the properties that you specify** – When you want to allow or block requests based on new properties in web requests, you first can configure AWS WAF to count the requests that match those properties without allowing or blocking those requests\. This lets you confirm that you didn't accidentally configure AWS WAF to block all the traffic to your website\. When you're confident that you specified the correct properties, you can change the behavior to allow or block requests\.

Using AWS WAF has several benefits:
+ Additional protection against web attacks using conditions that you specify\. You can define conditions by using characteristics of web requests such as the following:
  + IP addresses that requests originate from\.
  + Country that requests originate from\.
  + Values in request headers\.
  + Strings that appear in requests, either specific strings or string that match regular expression \(regex\) patterns\.
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

AWS Firewall Manager simplifies your administration and maintenance tasks across multiple accounts and resources for AWS WAF rules, AWS Shield Advanced protections, and Amazon VPC security groups\. The Firewall Manager service automatically applies your rules and other security protections across your accounts and resources, even as you add new accounts and resources\. 

For more information about Firewall Manager, see [AWS Firewall Manager](fms-chapter.md)\.