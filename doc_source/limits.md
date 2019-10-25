# AWS WAF Limits<a name="limits"></a>

AWS WAF has default limits on the number of entities per account\. You can [request an increase](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-waf) in these limits\.


| Resource | Default Limit | 
| --- | --- | 
| Web ACLs per AWS account per Region | 50 | 
| Rules per AWS account per Region | 100 | 
| Rate\-based\-rules per AWS account per Region | 5 | 
| Conditions per AWS account per Region | 100 of each condition type \(For example: 100 size constraint conditions, 100 IP match conditions, and so on\. The exception is regex match conditions\. You can have a maximum of 10 regex match conditions per account per Region\. This limit cannot be increased\.\) | 
| Requests per Second | 25,000 per web ACL\* | 

\*This limit applies only to AWS WAF on an Application Load Balancer\. Requests per Second \(RPS\) limits for AWS WAF on CloudFront are the same as the RPS limits support by CloudFront that is described in the [CloudFront Developer Guide](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/cloudfront-limits.html)\.

The following limits on AWS WAF entities can't be changed\.


| Resource | Limit | 
| --- | --- | 
| Rule groups per web ACL | 2: 1 customer\-created rule group and 1 AWS Marketplace rule group | 
| Rules per web ACL | 10 | 
| Conditions per rule | 10 | 
| IP address ranges \(in CIDR notation\) per IP match condition | 10,000 | 
| IP addresses blocked per rate\-based rule | 10,000 | 
| Minimum rate\-based rule rate limit per 5 minute period | 100 | 
| Filters per cross\-site scripting match condition | 10 | 
| Filters per size constraint condition | 10 | 
| Filters per SQL injection match condition | 10 | 
| Filters per string match condition | 10 | 
| In string match conditions, the number of characters in HTTP header names, when you've configured AWS WAF to inspect the headers in web requests for a specified value | 40 | 
| In string match conditions, the number of characters in the value that you want AWS WAF to search for | 50 | 
| In regex match conditions, the number of characters in the pattern that you want AWS WAF to search for | 70 | 
| In regex match conditions, the number of patterns per pattern set | 10 | 
| In regex match conditions, the number of pattern sets per regex condition | 1 | 
| The number of pattern sets per AWS account per Region | 5 | 
| GeoMatchSets per AWS account per Region | 50 | 
| Locations per GeoMatchSet | 50 | 