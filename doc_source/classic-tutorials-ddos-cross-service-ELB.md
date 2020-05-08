# Step 2: Scale your traffic using Elastic Load Balancing<a name="classic-tutorials-ddos-cross-service-ELB"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

Elastic Load Balancing provides additional protection against application layer attacks\. Elastic Load Balancing distributes traffic to multiple Amazon EC2 instances\. Using Elastic Load Balancing, along with CloudFront \(discussed later in this tutorial\), SSL negotiation is handled by the load balancer and CloudFront edge servers, which helps to protect your Amazon EC2 instances from SSL\-based attacks\. 

**Important**  
You are responsible for the cost of the AWS services implemented in this tutorial\. For full details about Elastic Load Balancing costs, see the [Elastic Load Balancing pricing page](https://aws.amazon.com/elasticloadbalancing/pricing/)\. 

**Topics**
+ [Before you begin](#classic-tutorials-ddos-cross-service-ELB-before)
+ [Create your load balancer](#classic-tutorials-ddos-cross-service-ELB-create)
+ [Test your load balancer](#classic-tutorials-ddos-cross-service-ELB-test)

## Before you begin<a name="classic-tutorials-ddos-cross-service-ELB-before"></a>

Ensure that the Amazon EC2 instances that you launched earlier in this tutorial are in the **Active** state\. 

## Create your load balancer<a name="classic-tutorials-ddos-cross-service-ELB-create"></a>

Next, you configure a load balancer that automatically routes traffic to your two Amazon EC2 instances\.

**To create a load balancer**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. On the navigation bar, select the same region that you selected for your EC2 instances\.

1. In the navigation pane, under **LOAD BALANCING**, choose **Target Groups**\.

1. Choose **Create target group**\.

1. Specify a name, protocol, port, and VPC for the target group, and then choose **Create**\. For this tutorial, use the following values:
   + **Name**: MyWebServers
   + **Protocol**: HTTP
   + **Port**: 80
   + **Target type**: Instance
   + **VPC**: The VPC that contains your EC2 instances
   + Keep the other settings\.

1. Select the new target group\.

1. On the **Targets** tab, choose **Edit**\.

1. For **Instances**, select both of the instances that you created earlier in this tutorial\. Choose **Add to registered**, and then choose **Save**\.

   The status of the instances is `initial` until the instances are registered and have passed health checks, and then it is `unused` until you configure the target group to receive traffic from the load balancer\.

1. In the navigation pane, under **LOAD BALANCING**, choose **Load Balancers**\.

1. Choose **Create Load Balancer**\.

1. For **Select load balancer type**, choose **Application Load Balancer**\.

1. Choose **Create**\.

1. Complete the **Configure Load Balancer** page as follows:

   1. For **Name**, type a name for your load balancer\.

   1. For **Scheme**, choose ** Internet\-facing**\. An internet\-facing load balancer routes requests from clients over the internet to targets\. An internal load balancer routes requests to targets using private IP addresses\.

   1. For **Listeners**, the default is a listener that accepts HTTP traffic on port 80\. 

   1. For **Availability Zones**, select the VPC that you used for your EC2 instances\. Select at least two Availability Zones\. If there is one subnet for an Availability Zone, it is selected\. If there is more than one subnet for an Availability Zone, select one of the subnets\. You can select only one subnet per Availability Zone\.

   1. Choose **Next: Configure Security Settings**\.

1. For now, ignore the message about creating a secure listener group\. Choose **Next: Configure Security Groups**\.

1. Complete the **Configure Security Groups** page as follows:

   1. Select **Create a new security group**\.

   1. Type a name and description for the security group, or keep the default name and description\. This new security group contains a rule that allows traffic to the port that you selected for your load balancer on the **Configure Load Balancer** page\.

   1. Choose **Next: Configure Routing**\.

1. Complete the **Configure Routing** page as follows:

   1. For **Target group**, choose **Existing target group**\.

   1. For **Name**, choose the target group that you created earlier\. 

   1. Choose **Next: Register Targets**\.

1. On the **Register Targets** page, the instances that you registered with the target group appear under **Registered instances**\. You can't modify the targets registered with the target group until after you complete the wizard\. Choose **Next: Review**\.

1. On the **Review** page, choose **Create**\.

1. After you are notified that your load balancer was created successfully, choose **Close**\.

## Test your load balancer<a name="classic-tutorials-ddos-cross-service-ELB-test"></a>

You should now be able to view your website using the DNS name of the load balancer\.

**To test your load balancer**

1. On the Amazon EC2 console, in the navigation pane, select **Load Balancers**\.

1. Select the box next to your load balancer\.

1. In the details pane, note the **DNS name**\.

1. Enter this address in a web browser\. You should be directed to your website\. 

**Important**  
If you make changes to the website, you must make the same changes to both EC2 instances\. The load balancer can serve content from either instance, so it is important that both instances are identical\.

Next: [Step 3: Improve performance and absorb attacks using Amazon CloudFront](classic-tutorials-ddos-cross-service-CF.md)\.