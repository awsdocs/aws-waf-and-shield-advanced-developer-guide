# AWS Shield Advanced protections by resource type<a name="ddos-protections-by-resource-type"></a>

Shield Advanced protects AWS resources in the network and transport layers \(layers 3 and 4\) and in the application layer \(layer 7\)\. You can protect some resources directly and others through association with protected resources\. This section provides information about Shield Advanced protections for each resource type\. 

**Note**  
Shield Advanced protects only resources that you have specified either in Shield Advanced or through an AWS Firewall Manager Shield Advanced policy\. It doesn't automatically protect your resources\.

You can use Shield Advanced for advanced monitoring and protection with the following resource types:
+ Amazon CloudFront distributions\. 
+ Amazon Route 53 hosted zones\.
+ AWS Global Accelerator standard accelerators\.
+ Amazon EC2 Elastic IP addresses\. Shield Advanced protects the resources that are associated with protected Elastic IP addresses\. 
+ Amazon EC2 instances, through association to Amazon EC2 Elastic IP addresses\. 
+ The following Elastic Load Balancing \(ELB\) load balancers:
  + Application Load Balancers\.
  + Classic Load Balancers\.
  + Network Load Balancers, through associations to Amazon EC2 Elastic IP addresses\. 

You can't use Shield Advanced to protect any other resource type\. For example you can't protect AWS Global Accelerator custom routing accelerators or Gateway Load Balancers\.

You can monitor and protect up to 1,000 resources for each resource type per AWS account\. For example, in a single account, you could protect 1,000 Amazon EC2 Elastic IP addresses, 1,000 CloudFront distributions, and 1,000 Application Load Balancers\. You can request an increase to the number of resources that you can protect with Shield Advanced through the Service Quotas console at [https://console\.aws\.amazon\.com/servicequotas/](https://console.aws.amazon.com/servicequotas/)\.

**Protecting Amazon EC2 instances and Network Load Balancers with Shield Advanced**  
You can protect Amazon EC2 instances and Network Load Balancers by first attaching these resources to Elastic IP addresses, and then protecting the Elastic IP addresses in Shield Advanced\.

When you protect Elastic IP addresses, Shield Advanced identifies and protects the resources that they're attached to\. Shield Advanced automatically identifies the type of resource that's attached to an Elastic IP address and applies the appropriate detections and mitigations for that resource\. This includes configuring network ACLs that are specific to the Elastic IP address\. For more information about using Elastic IP addresses with your AWS resources, see the following guides: [Amazon Elastic Compute Cloud documentation](https://docs.aws.amazon.com/ec2/) or [Elastic Load Balancing documentation](https://docs.aws.amazon.com/elasticloadbalancing/)\.

During an attack, Shield Advanced automatically deploys your network ACLs to the border of the AWS network\. When your network ACLs are at the border of the network, Shield Advanced can provide protection against larger DDoS events\. Typically, network ACLs are applied near your Amazon EC2 instances within your Amazon VPC\. The network ACL can mitigate attacks only as large as your Amazon VPC and instance can handle\. For example, if the network interface attached to your Amazon EC2 instance can process up to 10 Gbps, then volumes over 10 Gbps will slow down and possibly block traffic to that instance\. During an attack, Shield Advanced promotes your network ACL to the AWS border, which can process multiple terabytes of traffic\. Your network ACL is able to provide protection for your resource well beyond your network's typical capacity\. For more information about network ACLs, see [Network ACLs](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_ACLs.html)\. 

Some scaling tools, like AWS Elastic Beanstalk, don't allow you to automatically attach an Elastic IP address to a Network Load Balancer\. For those cases, you need to manually attach the Elastic IP address\.