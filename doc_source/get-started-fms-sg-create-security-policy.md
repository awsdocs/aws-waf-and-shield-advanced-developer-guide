# Step 3: Create and apply an AWS Firewall Manager common security group policy<a name="get-started-fms-sg-create-security-policy"></a>

After completing the prerequisites, you create an AWS Firewall Manager common security group policy\. A common security group policy provides a centrally controlled security group for your entire AWS organization\. It also defines the AWS accounts and resources that the security group applies to\. In addition to common security group policies, Firewall Manager supports content audit security group policies, to manage the security group rules in use in your organization, and usage audit security group policies, to manage unused and redundant security groups\. For more information, see [Security group policies](security-group-policies.md)\.

For this tutorial, you create a common security group policy and set its action to not automatically remediate\. This allows you to see what effect the policy would have without making changes to your AWS organization\.<a name="get-started-fms-sg-create-security-policy-procedure"></a>

**To create a Firewall Manager common security group policy \(console\)**

1. Sign in to the AWS Management Console using the AWS Firewall Manager administrator account that you set up in the prerequisites, and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 

1. In the navigation pane, choose **Security policies**\. 

1. If you have not met the prerequisites, the console displays instructions about how to fix any issues\. Follow the instructions, and then return to this step, to create a common security group policy\. 

1. Choose **Create policy**\.

1. For **Policy type**, choose **Security group**\. 

1. For **Security group policy type**, choose **Common security groups**\.

1. For **Region**, choose an AWS Region\. 

1. Choose **Next**\.

1. For **Policy name**, enter a friendly name\. 

1. **Policy rules** allow you to choose how the security groups in this policy are applied and maintained\. For this tutorial, choose **Disassociate any other security groups from AWS resources within the policy scope\.** and leave the other options unchecked\. 

1. Choose **Add primary security group**, select the security group that you created for this tutorial, and choose **Add security group**\.

1. For **Policy action**, choose **Identify resources that don’t comply with the policy rules, but don’t auto remediate\.** 

1. Choose **Next**\.

1. **AWS accounts this policy applies to** allows you to narrow the scope of your policy by specifying accounts to include or exclude\. For this tutorial, choose **Include all accounts under my organization\.** 

1. For **Resource type**, choose one or more types, according to the resources you have defined for your AWS organization\. 

   **Resources** allows you to narrow the scope of your policy by specifying resource tags for inclusion or exclusion\. To use tagging, you need to first tag your resources\. For more information about tagging your resources, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\. For this tutorial, choose **Include all resources that match the selected resource type**\. 

1. Choose **Next**\.

1. Review your policy settings\. Check to be sure that **Policy actions** is set to **Identify resources that don’t comply with the policy rules, but don’t auto remediate\.** This allows you to review the changes that your policy would have, without making changes at this time\.

1. Choose **Create policy**\.

   In the **AWS Firewall Manager policies** pane, your policy should be listed\. It will probably indicate **Pending** under the accounts headings and it will indicate that **Automatic remediation** is disabled\. The creation of a policy can take several minutes\. After the **Pending** status is replaced with account counts, you can choose the policy name to explore the compliance status of the accounts and resources\. For information, see [Viewing resource compliance for a policy](fms-compliance.md)

1. When you are finished exploring, if you don't want to keep the policy you created for this tutorial, choose the policy name, choose **Delete**, choose **Clean up resources created by this policy\.**, and finally choose **Delete**\. 

For more information about Firewall Manager security group policies, see [Security group policies](security-group-policies.md)\.
