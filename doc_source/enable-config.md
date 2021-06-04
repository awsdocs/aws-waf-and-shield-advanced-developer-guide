# Step 3: Enable AWS Config<a name="enable-config"></a>

To use Firewall Manager, you must enable AWS Config\. 

**Note**  
You incur charges for your AWS Config settings, according to AWS Config pricing\. For more information, see [Getting Started with AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/getting-started.html)\.

**To enable AWS Config for Firewall Manager**

1. Enable AWS Config for each of your AWS Organizations member accounts\. For more information, see [Getting Started with AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/getting-started.html)\.

1. Enable AWS Config for each AWS Region that contains the resources that you want to protect\. You can enable AWS Config manually, or you can use the AWS CloudFormation template "Enable AWS Config" at [AWS CloudFormation StackSets Sample Templates](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-sampletemplates.html)\. 

   If you don't want to enable AWS Config for all resources, then you must enable the following according to the type of Firewall Manager policies that you use: 
   + **WAF policy** – Enable Config for the resource types CloudFront Distribution, Application Load Balancer \(choose **ElasticLoadBalancingV2** from the list\), API Gateway, WAF WebACL, WAF Regional WebACL, and WAFv2 WebACL\. To enable AWS Config to protect a CloudFront distribution, you must be in the US East \(N\. Virginia\) Region\. Other Regions don't have CloudFront as an option\. 
   + **Shield policy** – Enable Config for the resource types Shield Protection, ShieldRegional Protection, Application Load Balancer, EC2 EIP, WAF WebACL, WAF Regional WebACL, and WAFv2 WebACL\. 
   + **Security group policy** – Enable Config for the resource types EC2 SecurityGroup, EC2 Instance, and EC2 NetworkInterface\.
   + **Network Firewall policy** – Enable Config for the resource types NetworkFirewall FirewallPolicy, NetworkFirewall RuleGroup, EC2 VPC, EC2 InternetGateway, EC2 RouteTable, and EC2 Subnet\. 
   + **DNS Firewall policy** – Enable Config for the resource types DNSFirewall RuleGroup and EC2 VPC\. 