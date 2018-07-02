# Step 3: Enable AWS Config<a name="enable-config"></a>

Enable AWS Config for each member account in your AWS organization\. For more information, see [Getting Started with AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/getting-started.html)\.

You must enable AWS Config for each AWS Region that contains the resources that you want to protect\. You can enable AWS Config manually, or you can use the AWS CloudFormation template "Enable AWS Config" at [AWS CloudFormation StackSets Sample Templates](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-sampletemplates.html)\.

You must, at a minimum, specify the following resource types that you want to protect with AWS Firewall Manager: Application Load Balancer, CloudFront distribution, or both\.

When enabling AWS Config to protect an Application Load Balancer, choose **ElasticLoadBalancingV2** in the provided list of resource types\. 

When enabling AWS Config to protect a CloudFront distribution, you must be in the US East \(N\. Virginia\) region\. Other regions will not have CloudFront as an option\.

You can now configure AWS Firewall Manager to begin protecting your resources\. For more information, see [Getting Started with AWS Firewall Manager](getting-started-fms.md) \.