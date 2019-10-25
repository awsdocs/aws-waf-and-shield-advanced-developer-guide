# Step 3: Enable AWS Config<a name="enable-config"></a>

To use Firewall Manager, you must enable AWS Config\. 

**Note**  
You incur charges for your AWS Config settings, according to AWS Config pricing\. For more information, see [Getting Started with AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/getting-started.html)\.

**To enable AWS Config for Firewall Manager \(console\)**

1. Enable AWS Config for each of your AWS Organizations member accounts\. For more information, see [Getting Started with AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/getting-started.html)\.

1. Enable AWS Config for each AWS Region that contains the resources that you want to protect\. You can enable AWS Config manually, or you can use the AWS CloudFormation template "Enable AWS Config" at [AWS CloudFormation StackSets Sample Templates](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-sampletemplates.html)\. At a minimum, you must specify one or both of the following resource types to protect with AWS Firewall Manager: 
   + Application Load Balancer – When enabling AWS Config to protect an Application Load Balancer, in the provided list of resource types, choose **ElasticLoadBalancingV2**\. 
   + CloudFront distribution – When enabling AWS Config to protect a CloudFront distribution, you must be in the US East \(N\. Virginia\) Region\. Other regions will not have CloudFront as an option\. 