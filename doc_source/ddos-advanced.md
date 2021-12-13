# AWS Shield Advanced<a name="ddos-advanced"></a>

For higher levels of protection against attacks, you can subscribe to AWS Shield Advanced\. When you subscribe to AWS Shield Advanced and add specific resources to be protected, AWS Shield Advanced provides expanded DDoS attack protection for web applications running on the resources\. 

**Note**  
AWS Shield Advanced only protects resources that you have specified either in Shield Advanced or through a AWS Firewall Manager Shield Advanced policy\. It doesn't automatically protect your resources\. 

You can add Shield Advanced protection for any of the following resource types:
+ Amazon CloudFront distributions
+ Amazon Route 53 hosted zones
+ AWS Global Accelerator accelerators
+ Application Load Balancers
+ Elastic Load Balancing \(ELB\) load balancers
+ Amazon Elastic Compute Cloud \(Amazon EC2\) Elastic IP addresses

**Protecting Network Load Balancers**  
You can't directly attach a Shield Advanced protection to a Network Load Balancer \(NLB\), but you can protect a Network Load Balancer by first associating an Amazon EC2 Elastic IP address to it and then adding the Elastic IP as a Shield Advanced protected resource\. Some scaling tools, like AWS Elastic Beanstalk, don't let you automatically attach an Elastic IP to a Network Load Balancer\. For those cases, you need to first associate the Elastic IP to the Network Load Balancer and then manually add the Shield Advanced protections to the Elastic IP\.

For example, if you use Shield Advanced to protect an Elastic IP address, Shield Advanced automatically deploys your network ACLs to the border of the AWS network during an attack\. When your network ACLs are at the border of the network, Shield Advanced can provide protection against larger DDoS events\. Typically, network ACLs are applied near your Amazon EC2 instances within your Amazon VPC\. The network ACL can mitigate attacks only as large as your Amazon VPC and instance can handle\. If the network interface attached to your Amazon EC2 instance can process up to 10 Gbps, volumes over 10 Gbps slow down and possibly block traffic to that instance\. During an attack, Shield Advanced promotes your network ACL to the AWS border, which can process multiple terabytes of traffic\. Your network ACL is able to provide protection for your resource well beyond your network's typical capacity\. For more information about network ACLs, see [Network ACLs](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_ACLs.html)\. 

When you protect a resource with Shield Advanced, Shield Advanced analyzes traffic over time to establish and maintain baselines\. It uses those baselines to detect anomalies in traffic patterns that might indicate a DDoS attack\. The point at which Shield Advanced detects attacks and sends notifications or places mitigations depends on the architecture you use for your web applications\. It varies based on characteristics like the type of instance you use, your instance size, and whether the instance type supports enhanced networking\. Shield Advanced doesn't automatically place mitigations for application layer \(layer 7\) attacks unless you've configured it to do so\.

As an AWS Shield Advanced customer, you can contact the 24x7 AWS Shield Response Team \(SRT\) for assistance during a DDoS attack\. You also have exclusive access to advanced, real\-time metrics and reports for extensive visibility into attacks on your AWS resources\. 

To use the services of the SRT, you must be subscribed to the [Business Support plan](https://aws.amazon.com/premiumsupport/business-support/) or the [Enterprise Support plan](https://aws.amazon.com/premiumsupport/enterprise-support/)\.

AWS Shield Advanced also offers some cost protection against spikes in your AWS bill that could result from a DDoS attack against your protected resources\. For information, see [Requesting a credit in AWS Shield Advanced](request-refund.md)\. 

AWS WAF is included with AWS Shield Advanced at no extra cost\. For more information about AWS Shield Advanced pricing, see [AWS Shield Advanced Pricing](http://aws.amazon.com/shield/pricing/)\.

AWS Shield Advanced protections include optional additions, which are described in the topics that follow\.

**Topics**
+ [Shield Advanced health\-based detection](ddos-advanced-health-check-option.md)
+ [Shield Advanced automatic application layer DDoS mitigation](ddos-advanced-automatic-app-layer-response.md)
+ [Shield Advanced proactive engagement](ddos-advanced-proactive-engagement.md)
+ [Shield Advanced protection groups](ddos-advanced-protection-groups.md)