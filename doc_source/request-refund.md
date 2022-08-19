# Requesting a credit in AWS Shield Advanced<a name="request-refund"></a>

If you're subscribed to AWS Shield Advanced and you experience a DDoS attack that increases utilization of a Shield Advanced protected resource, you can request a credit for charges related to the increased utilization to the extent that it is not mitigated by Shield Advanced\. Credits are available only for the following types of charges: Amazon CloudFront HTTP/HTTPS requests, CloudFront data transfer out, Amazon Route 53 queries, AWS Global Accelerator standard accelerator data transfer, load balancer capacity units for Application Load Balancer, and usage spikes on protected Amazon Elastic Compute Cloud \(Amazon EC2\) instances\.

**Prerequisites for requesting a credit**  
To be eligible to receive a credit, before the attack began, you must have done the following: 
+ You must have added Shield Advanced protection to the resources for which you want to request a credit\. Protected resources added during an attack are not eligible for cost protection\. 
**Note**  
Enabling Shield Advanced on your AWS account does not automatically enable Shield Advanced protection for individual resources\. 

  For more information about how to protect AWS resources using Shield Advanced, see [Adding AWS Shield Advanced protection to AWS resources](ddos-manage-protected-resources.md#configure-new-protection)\.
+ For applicable CloudFront and Application Load Balancer protected resources, you must have associated an AWS WAF web ACL and implemented a rate\-based rule in the web ACL\. For information about how to create AWS WAF rate\-based rules, see [Rate\-based rule statement](waf-rule-statement-type-rate-based.md)\. For information about how to associate web ACLs with AWS resources, see [Web access control lists \(web ACLs\)](web-acl.md)\. 
+ You must have implemented the appropriate best practices in [AWS Best Practices for DDoS Resiliency](https://docs.aws.amazon.com/whitepapers/latest/aws-best-practices-ddos-resiliency) to configure your application in a way that minimizes cost during a DDoS attack\. 

**How to apply for a credit**  
To be eligible for a credit, you must submit your credit request within 15 days of the end of the billing month in which the attack occurred\.

To apply for a credit, submit a billing case through the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\. Include the following in your request: 
+ The words "DDoS Concession" in the subject line
+ The dates and times of each event or availability interruption for which you're requesting a credit
+ The AWS services and specific resources that were affected 

After you submit a request, the AWS Shield Response Team \(SRT\) will validate whether a DDoS attack occurred and, if so, whether any protected resources scaled to absorb the DDoS attack\. If AWS determines that protected resources scaled to absorb the DDoS attack, AWS will issue a credit for that portion of traffic that AWS determines was caused by the DDoS attack\. Credits are valid for 12 months\.