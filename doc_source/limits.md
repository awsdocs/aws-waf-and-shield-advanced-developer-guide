# AWS WAF Limits<a name="limits"></a>

AWS WAF has default limits on the number of entities per account\. You can [request an increase](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-waf) in these limits\.


| Resource | Default Limit | 
| --- | --- | 
| Web ACLs per Region | 100 | 
| Rule groups per Region | 100 | 
| Web ACL capacity units \(WCUs\) per web ACL | 1,500 | 
| WCUs per rule group | 1,500 | 
| IP sets per Region | 100 | 
| Requests per second per web ACL \(applies only to Application Load Balancers\) | 10,000 | 

Requests per second \(RPS\) limit for AWS WAF on CloudFront is set by CloudFront and described in the [CloudFront Developer Guide](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/cloudfront-limits.html)\.

The following limits on AWS WAF entities can't be changed\.


| Resource | Default Limit | 
| --- | --- | 
| IP addresses in CIDR notation per IP set |  10,000  | 
| Unique IP addresses that can be blocked per rate\-based rule |  10,000  | 
| Maximum characters allowed for a string match statement |  200  | 
| Maximum characters allowed for each regex pattern |  200  | 
| Unique regex patterns per regex set | 10 | 
| Regex sets per Region | 10 | 
| Maximum size of a web request body that can be inspected |  8 KB  | 
| Rate\-based rules per web ACL | 10 | 
| Minimum request rate that can be defined for a rate\-based rule |  100  | 