# Step 3: Create and apply an AWS Firewall Manager Network Firewall policy<a name="get-started-fms-network-firewall-create-policy"></a>

After completing the prerequisites, you create an AWS Firewall Manager Network Firewall policy\. A Network Firewall policy provides a centrally controlled AWS Network Firewall firewall for your entire AWS organization\. It also defines the AWS accounts and resources that the firewall applies to\. 

For more information about how Firewall Manager manages your Network Firewall policies, see [AWS Network Firewall policies](network-firewall-policies.md)\.<a name="get-started-fms-network-firewall-create-policy-procedure"></a>

**To create a Firewall Manager Network Firewall policy \(console\)**

1. Sign in to the AWS Management Console using the AWS Firewall Manager administrator account that you set up in the prerequisites, and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 

1. In the navigation pane, choose **Security policies**\. 

1. If you haven't met the prerequisites, the console displays instructions about how to fix any issues\. Follow the instructions, and then return to this step, to create a Network Firewall policy\. 

1. Choose **Create security policy**\.

1. For **Policy type**, choose **AWS Network Firewall**\. 

1. For **Region**, choose an AWS Region\. 

1. Choose **Next**\.

1. For **Policy name**, enter a descriptive name\. 

1. The policy configuration allows you to define the firewall policy\. This is the same process as the one you use in the AWS Network Firewall console\. You add the rule groups that you want to use in your policy and provide the default stateless actions\. For this tutorial, configure this policy as you would a firewall policy in Network Firewall\. 

1. Choose **Next**\.

1. For **Firewall endpoints**, choose **Multiple firewall endpoints**\. This option provides high availability for your firewall\. When you create the policy, Firewall Manager creates a firewall subnet in each Availability Zone where you have public subnets to protect\. 

1. **AWS accounts affected by this policy** allows you to narrow the scope of your policy by specifying accounts to include or exclude\. For this tutorial, choose **Include all accounts under my organization**\. 

1. The **Resource type** for a Network Firewall policy is always **VPC**\. 

1. **Resources** allows you to narrow the scope of your policy by specifying resource tags for inclusion or exclusion\. To use tagging, you need to first tag your resources\. For more information about tagging your resources, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\. For this tutorial, choose **Include all resources that match the selected resource type**\. 

1. Choose **Next**\.

1. Review your policy settings, and then choose **Create policy**\.

   In the **AWS Firewall Manager policies** pane, your policy should be listed\. The creation of a policy can take several minutes\. Until the creation process is complete, the policy indicates that it's pending\. When the policy is ready, the status updates with the count of in\-scope accounts\. You can choose the policy name to explore the compliance status of the accounts and resources\. For information, see [Viewing compliance information for an AWS Firewall Manager policy](fms-compliance.md)

1. When you are finished exploring, if you don't want to keep the policy that you created for this tutorial, choose the policy name, choose **Delete**, choose **Clean up resources created by this policy\.**, and finally choose **Delete**\. 

For more information about Firewall Manager Network Firewall policies, see [AWS Network Firewall policies](network-firewall-policies.md)\.