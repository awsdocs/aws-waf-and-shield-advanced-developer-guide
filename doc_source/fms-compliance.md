# Viewing Resource Compliance with a Policy<a name="fms-compliance"></a>

You can check to see what resources an AWS Firewall Manager policy is being applied to\.<a name="fms-compliance-procedure"></a>

**To check what resources an AWS Firewall Manager policy is being applied to \(console\)**

1. Sign in to the AWS Management Console using the Firewall Manager administrator account that you set up in the prerequisites, and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [Step 2: Set the AWS Firewall Manager Administrator Account](enable-integration.md)\.

1. In the navigation pane, choose **Security policies**\.

1. Choose a policy\. Firewall Manager lists each account in the organization and shows the status\. A **Compliant** status indicates that the policy has been applied to all applicable resources in the account\. A **Noncompliant** status indicates that the policy is not applied to all resources in the account\.

1. Choose an account\. Firewall Manager lists each resource in the account and shows the status\. A **Compliant** status indicates that the policy is applied to the resource\. A **Noncompliant** status indicates that the policy is not applied to the resource\. Firewall Manager lists up to 100 noncompliant resources\.