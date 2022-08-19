# AWS WAF quotas<a name="limits"></a>

**Note**  
This is the latest version of AWS WAF\. For AWS WAF Classic, see [AWS WAF Classic](classic-waf-chapter.md)\.

AWS WAF is subject to the following quotas \(formerly referred to as limits\)\. These quotas are the same for all Regions in which AWS WAF is available\. Each Region is subject to these quotas individually\. The quotas are not cumulative across Regions\.

AWS WAF has default quotas on the maximum number of entities you can have per account\. You can [request an increase](https://console.aws.amazon.com/servicequotas/home/services/wafv2/quotas) in these quotas\.


| Resource | Default quota per account per Region | 
| --- | --- | 
|  Maximum number of web ACLs  |  100  | 
|  Maximum number of rule groups   |  100  | 
|  Maximum web ACL capacity units \(WCUs\) per web ACL  |  1,500  | 
| Maximum WCUs per rule group |  1,500  | 
| Maximum number of IP sets  |  100  | 
| Maximum number of requests per second per web ACL  |  25,000  | 
| Maximum number of custom request headers per web ACL or rule group | 100 | 
| Maximum number of custom response headers per web ACL or rule group | 100 | 
| Maximum number of custom response bodies per web ACL or rule group | 50 | 
| Maximum number of Amazon CloudWatch Logs log streams per web ACL, for logging web ACL traffic to an CloudWatch Logs log group | 35 | 

The maximum requests per second \(RPS\) allowed for AWS WAF on CloudFront is set by CloudFront and described in the [CloudFront Developer Guide](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/cloudfront-limits.html)\.

AWS WAF has fixed quotas on the following entity settings per account per Region\. These quotas can't be changed\.


| Resource | Quota per account per Region | 
| --- | --- | 
| Maximum number of references per rule group to IP sets and regex pattern sets |  50  | 
| Maximum number of references per web ACL to IP sets, regex pattern sets, and rule groups |  50  | 
| Maximum number of IP addresses in CIDR notation per IP set |  10,000  | 
| Maximum number of rate\-based rules per web ACL  |  10  | 
| Maximum number of rate\-based rules per rule group |  4  | 
| Maximum number of unique IP addresses that can be blocked per rate\-based rule |  10,000  | 
| Maximum number of characters in a string match statement |  200  | 
| Maximum number of characters in each regex pattern |  200  | 
| Maximum number of unique regex patterns per regex set |  10  | 
| Maximum number of regex sets  |  10  | 
| Maximum size of a web request body that can be inspected |  8 KB  | 
| Minimum request rate that can be defined for a rate\-based rule |  100  | 
| Maximum number of text transformations per rule statement |  3  | 
| Maximum size of the custom response body content for a single custom response definition |  4 KB  | 
| Maximum number of custom headers for a single custom response definition |  10  | 
| Maximum number of custom headers for a single custom request definition |  10  | 
| Maximum combined size of all response body content for a single rule group or a single web ACL |  50 KB  | 

AWS WAF has the following fixed quotas on calls per account per Region\. These quotas apply to the total calls to the service through any available means, including the console, CLI, AWS CloudFormation, the REST API, and the SDKs\. These quotas can't be changed\.


| Call type | Quota per account per Region | 
| --- | --- | 
| Maximum number of calls to AssociateWebACL |  One request every 2 seconds   | 
| Maximum number of calls to DisassociateWebACL |  One request every 2 seconds   | 
| Maximum number of calls to GetWebACLForResource  |  One request per second  | 
| Maximum number of calls to ListResourcesForWebACL |  One request per second  | 
| Maximum number of calls to any individual Get or List action, if no other quota is defined for it  |  Five requests per second  | 
| Maximum number of calls to any individual Create, Put, or Update action, if no other quota is defined for it  |  One request per second  | 