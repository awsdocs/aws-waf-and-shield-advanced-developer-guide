# AWS WAF quotas<a name="limits"></a>

**Note**  
This is the latest version of AWS WAF\. For AWS WAF Classic, see [AWS WAF Classic](classic-waf-chapter.md)\.

AWS WAF is subject to the following quotas \(formerly referred to as limits\)\. These quotas are the same for all Regions in which AWS WAF is available\. Each Region is subject to these quotas individually\. The quotas are not cumulative across Regions\.

AWS WAF has default quotas on the maximum number of entities you can have per account\. You can [request an increase](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-waf) in these quotas\.


| Resource | Default quota per account per Region | 
| --- | --- | 
|  Web ACLs  |  100  | 
|  Rule groups   |  100  | 
|  Web ACL capacity units \(WCUs\) per web ACL  |  1,500  | 
| WCUs per rule group |  1,500  | 
| IP sets  |  100  | 
| Requests per second per web ACL \(applies only to Application Load Balancers\) |  25,000  | 

The maximum requests per second \(RPS\) allowed for AWS WAF on CloudFront is set by CloudFront and described in the [CloudFront Developer Guide](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/cloudfront-limits.html)\.

AWS WAF has fixed quotas on the following entity settings per account per Region\. These quotas can't be changed\.


| Resource | Quota per account per Region | 
| --- | --- | 
| Maximum number of references \(to IP sets and regex pattern sets\) per rule group |  50  | 
| Maximum number of references \(to IP sets, regex pattern sets, and rule groups\) per web ACL |  50  | 
| IP addresses in CIDR notation per IP set |  10,000  | 
| Unique IP addresses that can be blocked per rate\-based rule |  10,000  | 
| Maximum characters allowed for a string match statement |  200  | 
| Maximum characters allowed for each regex pattern |  200  | 
| Unique regex patterns per regex set |  10  | 
| Regex sets  |  10  | 
| Maximum size of a web request body that can be inspected |  8 KB  | 
| Minimum request rate that can be defined for a rate\-based rule |  100  | 

AWS WAF has the following fixed quotas on calls per account per Region\. These quotas apply to the total calls to the service through any available means, including the console, CLI, AWS CloudFormation, the REST API, and the SDKs\. These quotas can't be changed\.


| Call type | Quota per account per Region | 
| --- | --- | 
| Maximum number of calls to AssociateWebACL |  One request every 2 seconds   | 
| Maximum number of calls to DisassociateWebACL |  One request every 2 seconds   | 
| Maximum number of calls to GetWebACLForResource  |  One request per second  | 
| Maximum number of calls to ListResourcesForWebACL |  One request per second  | 
| Maximum number of calls to any individual Get or List action, if no other quota is defined for it  |  Five requests per second  | 
| Maximum number of calls to any individual Create, Put, or Update action, if no other quota is defined for it  |  One request per second  | 