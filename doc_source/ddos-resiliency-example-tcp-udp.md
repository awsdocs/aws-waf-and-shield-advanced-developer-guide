# DDoS resiliency example for TCP and UDP applications<a name="ddos-resiliency-example-tcp-udp"></a>

This example shows a DDoS resilient architecture for TCP and UDP applications in an AWS Region that uses Amazon Elastic Compute Cloud \(Amazon EC2\) instances or Elastic IP \(EIP\) addresses\. 

You can follow this general example to improve DDoS resiliency for the following application types: 
+ TCP or UDP applications\. For example, applications used for gaming, IoT, and voice over IP\.
+ Web applications that require static IP addresses or that use protocols that Amazon CloudFront doesn't support\. For example, your application might require IP addresses that your users can add to their firewall allow lists, and that aren't used by any other AWS customers\.

You can improve DDoS resiliency for these application types by introducing Amazon Route 53 and AWS Global Accelerator\. These services can route users to your application and they can provide your application with static IP addresses that are anycast routed across the AWS global edge network\. Global Accelerator standard accelerators can improve user latency by up to 60%\. If you have a web application, you can detect and mitigate web application layer request floods by running the application on an Application Load Balancer, and then protecting the Application Load Balancer with an AWS WAF web ACL\.

After you've built your application, protect your Route 53 hosted zones, Global Accelerator standard accelerators, and any Application Load Balancers with Shield Advanced\. When you protect your Application Load Balancers, you can associate AWS WAF web ACLs and create rate\-based rules for them\. You can configure proactive engagement with the SRT for both your Global Accelerator standard accelerators and your Application Load Balancers by associating new or existing Route 53 health checks\. To learn more about the options, see [Resource protections in AWS Shield Advanced](ddos-resource-protections.md)\. 

The following reference diagram depicts an example DDoS resilient architecture for TCP and UDP applications\.

![\[The diagram shows users connected to Route 53 and to an AWS Global Accelerator. The accelerator is connected to an Elastic Load Balancing icon that's protected by AWS Shield Advanced and AWS WAF. The Elastic Load Balancing is itself connected to an Amazon EC2 instance. This Elastic Load Balancing instance and the Amazon EC2 instance are in Region 1. The AWS Global Accelerator is also directly connected to another Amazon EC2 instance, which isn't behind a protected Elastic Load Balancing intsance. This second Amazon EC2 instance is in Region n.\]](http://docs.aws.amazon.com/waf/latest/developerguide/)

The benefits that this approach provides to your application include the following:
+ Protection against the largest known infrastructure layer \(layer 3 and layer 4\) DDoS attacks\. If the volume of an attack causes congestion upstream from AWS, the failure will be isolated closer to its source and will have a minimized effect on your legitimate users\.
+ Protection against DNS application layer attacks, because Route 53 is responsible for serving authoritative DNS responses\. 
+ If you have a web application, this approach provides protection against web application layer request floods\. The rate\-based rule that you configure in your AWS WAF web ACL blocks source IPs while they are sending more requests than the rule allows\. 
+ Proactive engagement with the Shield Response Team \(SRT\), if you choose to enable this option for eligible resources\. When Shield Advanced detects an event that affects the health of your application, the SRT responds and proactively engages with your security or operations teams using the contact information that you provide\. 