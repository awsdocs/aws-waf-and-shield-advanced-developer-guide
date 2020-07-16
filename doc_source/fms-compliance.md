# Viewing resource compliance for a policy<a name="fms-compliance"></a>

For all policies, you can view the compliance status for in\-scope accounts and resources\. For content audit security group policies, you can also view detailed violation information for in scope resources\. This information can help you to better understand and manage your security risk\.<a name="fms-compliance-procedure"></a>

**To view the compliance information for a policy**

1. Sign in to the AWS Management Console using the Firewall Manager administrator account that you set up in the Firewall Manager prerequisites, and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [Step 2: Set the AWS Firewall Manager administrator account](enable-integration.md)\.

1. In the navigation pane, choose **Security policies**\.

1. Choose a policy\. In the **Accounts and resources** tab of the policy page, Firewall Manager lists the accounts in your organization, grouped by those that are within scope of the policy and those that are outside of scope\. 

   The **Accounts within policy scope** pane lists the compliancy status for each account\. A **Compliant** status indicates that the policy has successfully been applied to all of in\-scope resources for the account\. A **Noncompliant** status indicates that the policy hasn't been applied to one or more of the in\-scope resources for the account\. 

1. Choose an account that's noncompliant\. In the account page, Firewall Manager lists the ID and type for each noncompliant resource and the reason that the resource is in violation of the policy\. 
**Note**  
For the resource types `AWS::EC2::NetworkInterface` \(ENI\) and `AWS::EC2::Instance`, Firewall Manager might not show all of the noncompliant resources\. After you fix the ones that are displayed for the account, Firewall Manager might list additional noncompliant resources in the account page\. 

1. If the Firewall Manager policy type is a content audit security group policy, you can access detailed violation information for a resource\. 

   To view violation details, choose the resource\. 
**Note**  
Resources that Firewall Manager found to be noncompliant before the addition of the detailed resource violation page might not have violation details\.

   In the resource page, Firewall Manager lists specific details about the violation, according to resource type\. 
   + **`AWS::EC2::NetworkInterface` \(ENI\)** – Firewall Manager displays information about the security group that the resource doesn't comply with\. Choose the security group to see more detail about it\. 
   + **`AWS::EC2::Instance`** – Firewall Manager displays the ENI attached to the EC2 instance that's noncompliant\. It also displays information about the security group that the resources don't comply with\. Choose the security group to see more detail about it\. 
   + **`AWS::EC2::SecurityGroup`** – Firewall Manager displays the following violation details:
     + **Noncompliant security group rule** – The rule that's in violation, including its protocol, port range, IP CIDR range, and description\. 
     + **Referenced rule** – The audit security group rule that the noncompliant security group rule violates, with its details\. 
     + **Violation reasons** – Explanation of the noncompliance finding\.
     + **Remediation action** – Suggested action to take\. If Firewall Manager can't determine a safe remediation action, this field is blank\. 