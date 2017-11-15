# Tutorial: Implementing a DDoS\-resistant Website Using AWS Services<a name="tutorials-ddos-cross-service"></a>

This tutorial provides step\-by\-step instructions for setting up a website that is resistant to distributed denial of service \(DDoS\) attacks\. A DDoS attack can flood your website with traffic, prevent legitimate users from accessing the site, and even cause your site to crash due to the overwhelming traffic volume\.


+ [Overview](#tutorials-ddos-cross-service-overview)
+ [Architecture](#tutorials-ddos-cross-service-architecture)
+ [Prerequisites](tutorials-ddos-cross-service-prereq.md)
+ [Step 1: Launch a Virtual Server Using Amazon EC2](tutorials-ddos-cross-service-EC2.md)
+ [Step 2: Scale Your Traffic Using Elastic Load Balancing](tutorials-ddos-cross-service-ELB.md)
+ [Step 3: Improve Performance and Absorb Attacks Using Amazon CloudFront](tutorials-ddos-cross-service-CF.md)
+ [Step 4: Register Your Domain Name and Implement DNS Service Using Amazon Route 53](tutorials-ddos-cross-service-R53.md)
+ [Step 5: Detect and Filter Malicious Web Requests Using AWS WAF](tutorials-ddos-cross-service-WAF.md)
+ [Additional Best Practices](tutorials-ddos-cross-service-best-practices.md)

## Overview<a name="tutorials-ddos-cross-service-overview"></a>

This tutorial shows you how to use several AWS services together to build a resilient, highly secure website\. For example, you learn how to do the following:

+ Use load balancers and edge servers, which distribute traffic to multiple instances across regions and zones and help to protect your instances from SSL\-based attacks

+ Mitigate infrastructure \(layer 3 and layer 4\) DDoS attacks with techniques like overprovisioning your capacity 

+ Use a web application firewall to monitor HTTP and HTTPS requests and control access to your content

The tutorial shows how to integrate AWS services such as Amazon EC2, Elastic Load Balancing, CloudFront, Amazon Route 53, and AWS WAF\. Although the tutorial is designed as an end\-to\-end solution, you don’t have to complete every step if you’re already using some of those AWS services\. For example, if you’ve already registered your website domain with Amazon Route 53 and are using Amazon Route 53 as your DNS service, you can skip those steps\. 

The tutorial is intended to help you launch each AWS service quickly\. For that reason, it doesn't cover all possible options\. For detailed information about each service, see [AWS Documentation](docs.aws.amazon.com)\. For many of the steps, this tutorial provides specific values to enter\. Generally you should use those values\. However, in certain cases, such as domain name for your website, use what is appropriate for your needs\.

Each main step of the tutorial briefly describes the following:

+ What you are doing

+ Why you are doing it \(that is, how it contributes to your DDoS protection\)

+ How to do it 

**Important**  
You are responsible for the cost of the AWS services implemented in this tutorial\. For full details, see the pricing webest\-practicesage for each AWS service that you use in this solution\. You can find links to each service on the [Cloud Products page](https://aws.amazon.com/products)\.

## Architecture<a name="tutorials-ddos-cross-service-architecture"></a>

The following diagram shows the architecture deployed in this tutorial\.

![\[Architecture\]](http://docs.aws.amazon.com/waf/latest/developerguide/images/waf-tutorial-2a.png)

To get started go to [Prerequisites](tutorials-ddos-cross-service-prereq.md)\.