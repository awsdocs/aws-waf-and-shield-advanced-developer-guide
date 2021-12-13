# AWS Shield<a name="shield-chapter"></a>

AWS provides AWS Shield Standard and AWS Shield Advanced for protection against DDoS attacks\. AWS Shield Standard is automatically included at no extra cost beyond what you already pay for AWS WAF and your other AWS services\. For added protection against DDoS attacks, AWS offers AWS Shield Advanced\. AWS Shield Advanced provides expanded DDoS attack protection for your resources\. 

You can add Shield Advanced protection for any of the following resource types:
+ Amazon CloudFront distributions
+ Amazon Route 53 hosted zones
+ AWS Global Accelerator accelerators
+ Application Load Balancers
+ Elastic Load Balancing \(ELB\) load balancers
+ Amazon Elastic Compute Cloud \(Amazon EC2\) Elastic IP addresses

**Protecting Network Load Balancers**  
You can't directly attach a Shield Advanced protection to a Network Load Balancer \(NLB\), but you can protect a Network Load Balancer by first associating an Amazon EC2 Elastic IP address to it and then adding the Elastic IP as a Shield Advanced protected resource\. Some scaling tools, like AWS Elastic Beanstalk, don't let you automatically attach an Elastic IP to a Network Load Balancer\. For those cases, you need to first associate the Elastic IP to the Network Load Balancer and then manually add the Shield Advanced protections to the Elastic IP\.

**Topics**
+ [How AWS Shield works](ddos-overview.md)
+ [Example AWS Shield Advanced use cases](aws-shield-use-case.md)
+ [Getting started with AWS Shield Advanced](getting-started-ddos.md)
+ [Configuring Shield Response Team \(SRT\) support](ddos-edit-drt.md)
+ [Managing resource protections in AWS Shield Advanced](ddos-manage-protected-resources.md)
+ [Reviewing and responding to DDoS events](ddos-responding.md)
+ [Requesting a credit in AWS Shield Advanced](request-refund.md)
+ [Security in AWS Shield](shd-security.md)
+ [AWS Shield Advanced quotas](shield-limits.md)