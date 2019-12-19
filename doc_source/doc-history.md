# Document History<a name="doc-history"></a>

| Change | Description | Date | 
| --- |--- |--- |
| [AWS Firewall Manager integrated with AWS Security Hub](https://docs.aws.amazon.com/waf/latest/developerguide/fms-findings.html) | AWS Firewall Manager now creates findings for resources that are out of compliance and for attacks and sends them to AWS Security Hub\.  | December 18, 2019 | 
| [Release of AWS WAF version 2](https://docs.aws.amazon.com/waf/latest/developerguide/waf-chapter.html) | New version of the AWS WAF developer guide\. You can manage a web ACL or rule group in JSON format\. Expanded capabilities include logical rule statements, rule statement nesting, and full CIDR support for IP addresses and address ranges\. Rules are no longer AWS resources, but exist only in the context of a web ACL or rule group\. For existing customers, the prior version of the service is now called AWS WAF Classic\. In the APIs, SDKs, and CLIs, AWS WAF Classic retains its naming schemes and this latest version of AWS WAF is referred to with an added "V2" or "v2", depending on the context\. AWS WAF can't access AWS resources that were created in AWS WAF Classic\. To use those resources in AWS WAF, you need to migrate them\.  | November 25, 2019 | 
| [AWS Managed Rules rule groups for AWS WAF](https://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups.html) | Added AWS Managed Rules rule groups\. These are free of charge for AWS WAF customers\. | November 25, 2019 | 
| [AWS Firewall Manager support for Amazon Virtual Private Cloud security groups](https://docs.aws.amazon.com/waf/latest/developerguide/working-with-policies.html) | Added support for Amazon VPC security groups to Firewall Manager\. | October 10, 2019 | 
| [AWS Firewall Manager support for AWS Shield Advanced](https://docs.aws.amazon.com/waf/latest/developerguide/logging.html) | Added support for Shield Advanced to Firewall Manager\. | March 15, 2019 | 
| [Tutorial: Creating Hierarchical Policies](https://docs.aws.amazon.com/waf/latest/developerguide/logging.html) | Added tutorial on creating hierarchical policies in AWS Firewall Manager\. | February 11, 2019 | 
| [Rule\-level control in rule groups](https://docs.aws.amazon.com/waf/latest/developerguide/logging.html) | You can now exclude individual rules from AWS Marketplace rule groups, as well as your own rule groups\. | December 12, 2018 | 
| [AWS Shield Advanced support for AWS Global Accelerator](https://docs.aws.amazon.com/waf/latest/developerguide/logging.html) | Shield Advanced can now protect AWS Global Accelerator\. | November 26, 2018 | 
| [AWS WAF support for Amazon API Gateway](https://docs.aws.amazon.com/waf/latest/developerguide/logging.html) | AWS WAF now protects API Gateway APIs\. | October 25, 2018 | 
| [Expanded AWS Shield Advanced Getting Started wizard](https://docs.aws.amazon.com/waf/latest/developerguide/getting-started-ddos.html) | New wizard provides opportunity to create rate\-based rules and Amazon CloudWatch Events\. | August 31, 2018 | 
| [AWS WAF logging](https://docs.aws.amazon.com/waf/latest/developerguide/logging.html) | Enable logging to get detailed information about traffic that is analyzed by your web ACL\. | August 31, 2018 | 
| [Support for query parameters in conditions](https://docs.aws.amazon.com/waf/latest/developerguide/waf-rule-statement-request-component.html) | When creating a condition, you can now search the requests for specific parameters\. | June 5, 2018 | 
| [Shield Advanced Getting Started Wizard](https://docs.aws.amazon.com/waf/latest/developerguide/getting-started-ddos.html) | Introduces a new streamlined process for subscribing to AWS Shield Advanced\. | June 5, 2018 | 
| [Expanded allowed CIDR ranges](https://docs.aws.amazon.com/waf/latest/developerguide/waf-rule-statement-type-ipset-match.html) | When creating an IP match condition, AWS WAF now supports IPv4 address ranges: /8 and any range between /16 through /32\.  | June 5, 2018 | 

## Earlier updates<a name="doc-history-early-changes"></a>

The following table describes important changes in each release of the *AWS WAF Developer Guide*\.


| Change | API Version | Description | Release Date | 
| --- | --- | --- | --- | 
| Update | 2016\-08\-24 | AWS Marketplace rule groups | November, 2017 | 
| Update | 2016\-08\-24 | Shield Advanced support for Elastic IP addresses | November, 2017 | 
| Update | 2016\-08\-24 | Global threat environment dashboard | November, 2017 | 
| Update | 2016\-08\-24 | DDoS\-resistant website tutorial | October, 2017 | 
| Update | 2016\-08\-24 | Geo and regex conditions | October, 2017 | 
| Update | 2016\-08\-24 | Rate\-based rules | June, 2017 | 
| Update | 2016\-08\-24 | Reorganization | April, 2017 | 
| Update | 2016\-08\-24 | Added information about DDOS protection and support for Application Load Balancers\. | November, 2016 | 
| New Features | 2015\-08\-24 |  You can now log all your API calls to AWS WAF through AWS CloudTrail, the AWS service that records API calls for your account and delivers log files to your S3 bucket\. CloudTrail logs can be used to enable security analysis, track changes to your AWS resources, and aid in compliance auditing\. Integrating AWS WAF and CloudTrail lets you determine which requests were made to the AWS WAF API, the source IP address from which each request was made, who made the request, when it was made, and more\. If you are already using AWS CloudTrail, you will start seeing AWS WAF API calls in your AWS CloudTrail log\. If you haven't turned on AWS CloudTrail for your account, you can turn on CloudTrail from the [AWS Management Console](https://console.aws.amazon.com/cloudtrail/home)\. There is no additional charge for turning on CloudTrail, but standard rates for Amazon S3 and Amazon SNS usage apply\.  | April 28, 2016 | 
| New Features | 2015\-08\-24 |  You can now use AWS WAF to allow, block, or count web requests that appear to contain malicious scripts, known as cross\-site scripting or XSS\. Attackers sometimes insert malicious scripts into web requests in an effort to exploit vulnerabilities in web applications\. For more information, see [Cross\-Site Scripting Attack Rule Statement](waf-rule-statement-type-xss-match.md)\.  |  March 29, 2016  | 
| New Features | 2015\-08\-24 |  With this release, AWS WAF adds the following features: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/waf/latest/developerguide/doc-history.html)  |  January 27, 2016  | 
| New Feature | 2015\-08\-24 |  You can now use the AWS WAF console to choose the CloudFront distributions that you want to associate a web ACL with\. For more information, see [Associating or Disassociating a Web ACL and a CloudFront Distribution](https://docs.aws.amazon.com/waf/latest/developerguide/web-acl-working-with.html#web-acl-associating-aws-resource)\.  |  November 16, 2015  | 
| Initial Release | 2015\-08\-24 |  This is the first release of the *AWS WAF Developer Guide*\.  |  October 6, 2015  | 