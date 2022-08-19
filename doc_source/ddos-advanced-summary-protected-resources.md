# AWS Shield Advanced protected resources<a name="ddos-advanced-summary-protected-resources"></a>

**Note**  
Shield Advanced protections are only enabled for resources that you have explicitly specified in Shield Advanced or that you protect through an AWS Firewall Manager Shield Advanced policy\. Shield Advanced doesn't automatically protect your resources\. 

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

For additional information about protections for these resource types, see [AWS Shield Advanced protections by resource type](ddos-protections-by-resource-type.md)\.