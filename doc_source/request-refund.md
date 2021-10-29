# Requesting a credit in AWS Shield Advanced<a name="request-refund"></a>

If you're subscribed to AWS Shield Advanced and you experience a DDoS attack that increases utilization of an Shield Advanced protected resource, you can request a credit for charges related to the increased utilization to the extent that it is not mitigated by Shield Advanced\. Credits are available only for increased charges that result directly from a DDoS attack in the following areas: Amazon CloudFront HTTP/HTTPS requests, CloudFront data transfer out, Amazon Route 53 queries, AWS Global Accelerator data transfer, load balancer capacity units for Application Load Balancer, and usage spikes on protected Amazon Elastic Compute Cloud \(Amazon EC2\) instances\.

To be eligible to receive a credit, before the attack began, you must have done the following for the resources for which you want a credit: 
+ Added Shield Advanced protection to the resources\. Protected resources added during an attack are not eligible for cost protection\. Enabling Shield Advanced on your AWS account does not automatically enable Shield Advanced protection for individual resources\. For more information about how to protect AWS resources using Shield Advanced, see [Adding AWS Shield Advanced protection to AWS resources](configure-new-protection.md)\.
+ Associated an AWS WAF web ACL with applicable CloudFront and Application Load Balancer protected resources\. For more information about how to associate web ACLs with AWS resources, see [Managing and using a web access control list \(web ACL\)](web-acl.md)\. 
+ Defined an AWS WAF rate\-based rule in block mode for applicable CloudFront and Application Load Balancer protected resources\. For more information about how to create AWS WAF rate\-based rules, see [Rate\-based rule statement](waf-rule-statement-type-rate-based.md)\.
+ Implemented applicable best practices, according to the guidance at [AWS Best Practices for DDoS Resiliency](https://d1.awsstatic.com/whitepapers/Security/DDoS_White_Paper.pdf), to configure your application in a way that minimizes cost during a DDoS attack\. 

To apply for a credit, submit a billing case through the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\. Be sure to include the following in your request: 
+ The words "DDoS Concession" in the subject line
+ The dates and times of each event interruption for which you're requesting a credit
+ The AWS services and specific resources that were affected 

**Important**  
To be eligible for a credit, you must submit your credit request within 15 days of the end of the billing month in which the attack occurred\.

After you submit a request, the AWS Shield Response Team \(SRT\) will validate whether a DDoS attack occurred and, if so, whether any protected resources scaled to absorb the attack\. If AWS determines that protected resources scaled to absorb the DDoS attack, AWS will issue a credit for that portion of traffic that AWS determines was caused by the attack\. Credits are valid for 12 months\.