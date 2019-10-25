# Security Group Policy Use Cases<a name="security-group-policies-use-cases"></a>

You can use AWS Firewall Manager common security group policies to automate the host firewall configuration for communication between Amazon VPC instances\. This section lists standard Amazon VPC architectures and describes how to secure each using Firewall Manager common security group policies\. These security group policies can help you apply a unified set of rules to select resources in different accounts and avoid per\-account configurations in Amazon Elastic Compute Cloud and Amazon VPC\. 

With Firewall Manager common security group policies, you can tag just the EC2 elastic network interfaces that you need to for communication with instances in another Amazon VPC\. The other instances in the same Amazon VPC are then more secure and isolated\. 

**Use Case: Internet\-accessible, public Amazon VPC**  
You can use a Firewall Manager common security group policy to secure a public Amazon VPC, for example, to allow only inbound port 443\. This is the same as only allowing inbound HTTPS traffic for a public VPC\. You can tag public resources within the VPC \(for example, as "PublicVPC"\), and then set the Firewall Manager policy scope to only resources with that tag\. Firewall Manager automatically applies the policy to those resources\.

**Use Case: Public and Private Amazon VPC instances**  
You can use the same common security group policy for public resources as recommended in the prior use case for internet\-accessible, public Amazon VPC instances\. You can use a second common security group policy to limit communication between the public resources and the private ones\. Tag the resources in the public and private Amazon VPC instances with something like "PublicPrivate" to apply the second policy to them\. You can use a third policy to define the allowed communication between the private resources and other corporation or private Amazon VPC instances\. For this policy, you can use another identifying tag on the private resources\. 

**Use Case: Hub and spoke Amazon VPC instances**  
You can use a common security group policy to define communications between the hub Amazon VPC instance and spoke Amazon VPC instances\. You can use a second policy to define communication from each spoke Amazon VPC instance to the hub Amazon VPC instance\. 

**Use Case: Default network interface for Amazon EC2 instances**  
You can use a common security group policy to allow only standard communications, for example internal SSH and patch/OS update services, and to disallow other insecure communication\. 

**Use Case: Identify resources with open permissions**  
You can use an audit security group policy to identify all resources within your organization that have permission to communicate with public IP addresses or that have IP addresses that belong to third\-party vendors\.