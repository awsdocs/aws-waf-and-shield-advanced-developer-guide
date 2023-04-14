# Step 3: Create and apply a DNS Firewall policy<a name="get-started-fms-dns-firewall-create-policy"></a>

After completing the prerequisites, you create an AWS Firewall Manager DNS Firewall policy\. A DNS Firewall policy provides a set of centrally controlled DNS Firewall rule group associations for your entire AWS organization\. It also defines the AWS accounts and resources that the firewall applies to\. 

For more information about how Firewall Manager manages your DNS Firewall rule group associations, see [Amazon Route 53 Resolver DNS Firewall policies](dns-firewall-policies.md)\.

**To create a Firewall Manager DNS Firewall policy \(console\)**

1. Sign in to the AWS Management Console using your Firewall Manager administrator account, and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fmsv2](https://console.aws.amazon.com/wafv2/fmsv2)\. 

1. In the navigation pane, choose **Security policies**\. 

1. If you haven't met the prerequisites, the console displays instructions about how to fix any issues\. Follow the instructions, and then return to this step, to create a DNS Firewall policy\. 

1. Choose **Create security policy**\.

1. For **Policy type**, choose **Amazon Route 53 Resolver DNS Firewall**\. 

1. For **Region**, choose an AWS Region\. 

1. Choose **Next**\.

1. For **Policy name**, enter a descriptive name\. 

1. The policy configuration allows you to define the DNS Firewall rule group associations that you want to manage from Firewall Manager\. You add the rule groups that you want to use in your policy\. You can define an association to evaluate first for your VPCs and one to evaluate last\. For this tutorial, add one or two rule group associations, depending on your needs\. 

1. Choose **Next**\.

1. **AWS accounts affected by this policy** allows you to narrow the scope of your policy by specifying accounts to include or exclude\. For this tutorial, choose **Include all accounts under my organization**\. 

1. The **Resource type** for a DNS Firewall policy is always **VPC**\. 

1. **Resources** allows you to narrow the scope of your policy by specifying resource tags for inclusion or exclusion\. To use tagging, you need to first tag your resources\. For more information about tagging your resources, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\. For this tutorial, choose **Include all resources that match the selected resource type**\. 

1. Choose **Next**\.

1. Review your policy settings, and then choose **Create policy**\.

   In the **AWS Firewall Manager policies** pane, your policy should be listed\. The creation of a policy can take several minutes\. Until the creation process is complete, the policy indicates that it's pending\. When the policy is ready, the status updates with the count of in\-scope accounts\. You can choose the policy name to explore the compliance status of the accounts and resources\. For information, see [Viewing compliance information for an AWS Firewall Manager policy](fms-compliance.md)

1. When you are finished exploring, if you don't want to keep the policy that you created for this tutorial, choose the policy name, choose **Delete**, choose **Clean up resources created by this policy\.**, and finally choose **Delete**\. 

For more information about Firewall Manager DNS Firewall policies, see [Amazon Route 53 Resolver DNS Firewall policies](dns-firewall-policies.md)\.