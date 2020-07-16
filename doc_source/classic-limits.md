# AWS WAF Classic quotas<a name="classic-limits"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

AWS WAF Classic is subject to the following quotas \(formerly referred to as limits\)\. 

AWS WAF Classic has default quotas on the number of entities per account per Region\. You can [request an increase](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-waf) to these\.


| Resource | Default quota per account per Region | 
| --- | --- | 
| Web ACLs  | 50 | 
| Rules  | 100 | 
| Rate\-based\-rules  | 5 | 
| Conditions  | 100 of each condition type \(For example: 100 size constraint conditions, 100 IP match conditions, and so on\. The exception is regex match conditions\. You can have a maximum of 10 regex match conditions per account per Region\. This quota cannot be increased\.\) | 
| Requests per Second | 25,000 per web ACL\* | 

\*This quota applies only to AWS WAF Classic on an Application Load Balancer\. Requests per Second \(RPS\) quotas for AWS WAF Classic on CloudFront are the same as the RPS quotas support by CloudFront that is described in the [CloudFront Developer Guide](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/cloudfront-limits.html)\.

The following quotas on AWS WAF Classic entities can't be changed\.


| Resource | Quota per account per Region | 
| --- | --- | 
| Rule groups per web ACL | 2: 1 customer\-created rule group and 1 AWS Marketplace rule group | 
| Rules per web ACL | 10 | 
| Conditions per rule | 10 | 
| IP address ranges \(in CIDR notation\) per IP match condition | 10,000You can update up to 1,000 addresses at a time\. The API call `UpdateIPSet` accepts a maximum of 1,000 addresses in a single request\. | 
| IP addresses blocked per rate\-based rule | 10,000 | 
| Minimum rate\-based rule rate limit per 5 minute period | 100 | 
| Filters per cross\-site scripting match condition | 10 | 
| Filters per size constraint condition | 10 | 
| Filters per SQL injection match condition | 10 | 
| Filters per string match condition | 10 | 
| In string match conditions, the number of characters in HTTP header names, when you've configured AWS WAF Classic to inspect the headers in web requests for a specified value | 40 | 
| In string match conditions, the number of characters in the value that you want AWS WAF Classic to search for | 50 | 
| In regex match conditions, the number of characters in the pattern that you want AWS WAF Classic to search for | 70 | 
| In regex match conditions, the number of patterns per pattern set | 10 | 
| In regex match conditions, the number of pattern sets per regex condition | 1 | 
| The number of pattern sets  | 5 | 
| GeoMatchSets  | 50 | 
| Locations per GeoMatchSet | 50 | 

AWS WAF Classic has the following fixed quotas on calls per account per Region\. These quotas apply to the total calls to the service through any available means, including the console, CLI, AWS CloudFormation, the REST API, and the SDKs\. These quotas can't be changed\.


| Call type | Quota per account per Region | 
| --- | --- | 
| Maximum number of calls to AssociateWebACL |  1 request every 2 seconds   | 
| Maximum number of calls to DisassociateWebACL |  1 request every 2 seconds   | 
| Maximum number of calls to GetWebACLForResource  |  1 request per second  | 
| Maximum number of calls to ListResourcesForWebACL |  1 request per second  | 
| Maximum number of calls to CreateWebACLMigrationStack |  1 request per second  | 
| Maximum number of calls to GetChangeToken |  10 requests per second  | 
| Maximum number of calls to GetChangeTokenStatus |  1 request per second  | 
| Maximum number of calls to any individual List action, if no other quota is defined for it  |  5 requests per second  | 
| Maximum number of calls to any individual Create, Put, Get, or Update action, if no other quota is defined for it  |  1 request per second  | 