# Additional best practices<a name="classic-tutorials-ddos-cross-service-best-practices"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

You now have several components in place to help protect your website from DDoS attacks\. However, there is still more you can do\. Following are several best practices you should consider\. This tutorial does not cover the implementation details of the best practices, but links to relevant documentation are provided\.

**Topics**
+ [Obscuring AWS resources](#classic-tutorials-ddos-cross-service-best-practices-obscure)
+ [Using security groups](#classic-tutorials-ddos-cross-service-best-practices-SG)
+ [Network access control lists \(ACLs\)](#classic-tutorials-ddos-cross-service-best-practices-ACL)
+ [Protecting your origin](#classic-tutorials-ddos-cross-service-best-practices-origin)
+ [Conclusion](#classic-tutorials-ddos-cross-service-best-practices-conclusion)

## Obscuring AWS resources<a name="classic-tutorials-ddos-cross-service-best-practices-obscure"></a>

For many website applications, your AWS resources do not need to be fully exposed to the internet\. For example, it might not be necessary for Amazon EC2 instances behind an elastic load balancer \(ELB\) to be publicly accessible\. In this scenario, you might decide to allow users to access the ELB on certain TCP ports and to allow only the ELB to communicate with the Amazon EC2 instances\. You can do this by configuring security groups and network access control lists \(ACLs\) within your Amazon Virtual Private Cloud \(VPC\)\. Amazon VPC allows you to provision a logically isolated section of the AWS Cloud where you can launch AWS resources in a virtual network that you define\.

Security groups and network ACLs are similar in that they allow you to control access to AWS resources within your Amazon VPC\. Security groups allow you to control inbound and outbound traffic at the instance level\. Network ACLs offer similar capabilities, but at the VPC subnet level\. Additionally, there is no charge for inbound data transfer on Amazon EC2 security group rules or network ACLs\. This ensures that you do not incur any additional charges for traffic that is dropped by your security groups or network ACLs\. 

## Using security groups<a name="classic-tutorials-ddos-cross-service-best-practices-SG"></a>

You can specify security groups when launching an Amazon EC2 instance or associate the instance with a security group later on\. All traffic to a security group from the internet is implicitly denied unless you create an `Allow` rule to permit the traffic\. For example, in this tutorial, you created a solution that consists of an ELB and two Amazon EC2 instances\. You should consider creating one security group for the ELB \("ELB security group"\) and one for the instances \("web application server security group"\)\. You can then create `Allow` rules to permit traffic from the internet to the ELB security group and to permit traffic from the ELB security group to the web application server security group\. As a result, traffic from the internet is unable to directly communicate with your Amazon EC2 instances, which makes it more difficult for an attacker to learn about the design and structure of your website\.

## Network access control lists \(ACLs\)<a name="classic-tutorials-ddos-cross-service-best-practices-ACL"></a>

With network ACLs, you can specify both `Allow` and `Deny` rules\. This is useful in case you want to explicitly deny certain types of traffic to your website\. For example, you can define IP addresses \(as CIDR ranges\), protocols, and destination ports that should be denied for the entire subnet\. If your website is used only for TCP traffic, you can create a rule to deny all UDP traffic, or vice versa\. This tool is useful when responding to DDoS attacks because it can allow you to create your own rules to mitigate the attack if you know the source IP addresses or other signature\. You can use network ACLs in conjunction with AWS WAF Classic ACLs\.

## Protecting your origin<a name="classic-tutorials-ddos-cross-service-best-practices-origin"></a>

You should consider configuring CloudFront to prevent users from bypassing CloudFront and requesting content directly from your origin\. This can improve the security of your origin\. To learn more, see [Using Custom Headers to Restrict Access to Your Content on a Custom Origin](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/forward-custom-headers.html#forward-custom-headers-restrict-access)\.

## Conclusion<a name="classic-tutorials-ddos-cross-service-best-practices-conclusion"></a>

The best practices outlined in this tutorial can help you to build a DDoS\-resilient architecture that can protect the availability of your website against many common infrastructure and application layer DDoS attacks\. The degree to which you are able to architect your application according to these best practices influences the type and volume of DDoS attacks that you can mitigate\. 

For more information, see the following:
+ [AWS Best Practices for DDoS Resiliency](https://d1.awsstatic.com/whitepapers/Security/DDoS_White_Paper.pdf)
+ [AWS Documentation](https://docs.aws.amazon.com)