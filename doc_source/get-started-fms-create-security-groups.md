# Step 2: Create a security group to use in your policy<a name="get-started-fms-create-security-groups"></a>

In this step, you create a security group that you could apply across your organization using Firewall Manager\. 

**Note**  
For this tutorial, you won't apply your security group policy to the resources in your organization\. You'll just create the policy and see what would happen if you applied the policy's security group to your resources\. You do this by disabling automatic remediation on the policy\.

If you already have a general security group defined, skip this step and go to [Step 3: Create and apply an AWS Firewall Manager common security group policy](get-started-fms-sg-create-security-policy.md)\. <a name="get-started-fms-create-security-groups-procedure"></a>

**To create a security group to use in an Firewall Manager common security group policy**
+ Create a security group that you could apply to all accounts and resources in your organization, following the guidance under [Security Groups for Your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html) in the [Amazon VPC User Guide](https://docs.aws.amazon.com/vpc/latest/userguide/)\.

  For information on the security group rules options, see [Security Group Rules Reference](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/security-group-rules-reference.html)\.

You are now ready to go to [Step 3: Create and apply an AWS Firewall Manager common security group policy](get-started-fms-sg-create-security-policy.md)\.