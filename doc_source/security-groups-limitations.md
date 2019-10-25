# Security Group Policy Limitations<a name="security-groups-limitations"></a>

 This section lists the limitations for using AWS Firewall Manager policies:
+ Updating security groups for Amazon EC2 elastic network interfaces that were created using the Fargate service type is not supported\. You can, however, update security groups for Amazon ECS elastic network interfaces with the Amazon EC2 service type\. 
+ Updating Amazon ECS elastic network interfaces is possible only for Amazon ECS services that use the rolling update \(Amazon ECS\) deployment controller\. For other Amazon ECS deployment controllers such as CODE\_DEPLOY or external controllers, Firewall Manager currently can't update the elastic network interfaces\. 
+ Firewall Manager doesn't currently support updating security groups in elastic network interfaces for an Elastic Load Balancing load balancer, an Application Load Balancer, or a Network Load Balancer\. 