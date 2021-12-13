# Viewing compliance information for an AWS Firewall Manager policy<a name="fms-compliance"></a>

Third\-party auditors assess the security and compliance of AWS services as part of multiple AWS compliance programs, such as SOC, PCI, FedRAMP, and HIPAA\.

To learn whether AWS WAF or other AWS services are in scope of specific compliance programs, see [AWS Services in Scope by Compliance Program](http://aws.amazon.com/compliance/services-in-scope/)\. For general information, see [AWS Compliance Programs](http://aws.amazon.com/compliance/programs/)\.

You can download third\-party audit reports using AWS Artifact\. For more information, see [Downloading Reports in AWS Artifact](https://docs.aws.amazon.com/artifact/latest/ug/downloading-documents.html)\.

Your compliance responsibility when using AWS services is determined by the sensitivity of your data, your company's compliance objectives, and applicable laws and regulations\. AWS provides the following resources to help with compliance:
+ [Security and Compliance Quick Start Guides](http://aws.amazon.com/quickstart/?awsf.quickstart-homepage-filter=categories%23security-identity-compliance) – These deployment guides discuss architectural considerations and provide steps for deploying baseline environments on AWS that are security and compliance focused\.
+ [Architecting for HIPAA Security and Compliance Whitepaper ](https://d0.awsstatic.com/whitepapers/compliance/AWS_HIPAA_Compliance_Whitepaper.pdf) – This whitepaper describes how companies can use AWS to create HIPAA\-compliant applications\.
**Note**  
Not all services are compliant with HIPAA\.
+ [AWS Compliance Resources](http://aws.amazon.com/compliance/resources/) – This collection of workbooks and guides might apply to your industry and location\.
+ [Evaluating Resources with Rules](https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config.html) in the *AWS Config Developer Guide* – The AWS Config service assesses how well your resource configurations comply with internal practices, industry guidelines, and regulations\.
+ [AWS Security Hub](https://docs.aws.amazon.com/securityhub/latest/userguide/what-is-securityhub.html) – This AWS service provides a comprehensive view of your security state within AWS that helps you check your compliance with security industry standards and best practices\.
+ [AWS Audit Manager](https://docs.aws.amazon.com/audit-manager/latest/userguide/what-is.html) – This AWS service helps you continuously audit your AWS usage to simplify how you manage risk and compliance with regulations and industry standards\.

For all AWS Firewall Manager policies, you can view the compliance status for accounts and resources that are in scope of the policy\. An account or resource is in compliance with a Firewall Manager policy if the settings in the policy are reflected in the settings for the account or resource\. Each policy type has its own compliance requirements, which you can tune when you define the policy\. For some policies, you can also view detailed violation information for in scope resources, to help you to better understand and manage your security risk\.

<a name="fms-compliance-procedure"></a>

**To view the compliance information for a policy**

1. Sign in to the AWS Management Console using your Firewall Manager administrator account, and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fmsv2](https://console.aws.amazon.com/wafv2/fmsv2)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [AWS Firewall Manager prerequisites](fms-prereq.md)\.

1. In the navigation pane, choose **Security policies**\.

1. Choose a policy\. In the **Accounts and resources** tab of the policy page, Firewall Manager lists the accounts in your organization, grouped by those that are within scope of the policy and those that are outside of scope\. 

   The **Accounts within policy scope** pane lists the compliancy status for each account\. A **Compliant** status indicates that the policy has successfully been applied to all of in\-scope resources for the account\. A **Noncompliant** status indicates that the policy hasn't been applied to one or more of the in\-scope resources for the account\. 

1. Choose an account that's noncompliant\. In the account page, Firewall Manager lists the ID and type for each noncompliant resource and the reason that the resource is in violation of the policy\. 
**Note**  
For the resource types `AWS::EC2::NetworkInterface` \(ENI\) and `AWS::EC2::Instance`, Firewall Manager might show a limited number of noncompliant resources\. To list additional noncompliant resources, fix the ones that are initially displayed for the account\.

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
   + **`AWS::EC2::Subnet`** – This is used for Network Firewall policies\. Firewall Manager displays the subnet ID, VPC ID, and Availability Zone\. If applicable, Firewall Manager includes additional information about the violation, for example the reason the violation occurred, or the ID of the route table a subnet should be associated with\. The violation description component contains a description of the expected state of the resource, the current, noncompliant state, and if available, a description of what caused the discrepancy\. 

     For example, the expected state of a subnet might be “Subnet should contain a AWS Network Firewall subnet in its availability zone”, the current state might be “subnet with id subnet\-1234 is missing a Network Firewall subnet in availability zone us\-east\-1e”, and the description might be “Firewall Manager was unable to create a subnet in this AZ because there are no available CIDR blocks\.”
     + **Route management violations** – For Network Firewall policies that use Monitor mode, Firewall Manager displays basic subnet information, as well as expected and actual routes in the subnet, internet gateway, and Network Firewall subnet route table\. Firewall Manager alerts you that there's a violation if the actual routes don’t match the expected routes in the route table\. 
     + **Remediation actions for route management violations** – For Network Firewall policies that use Monitor mode, Firewall Manager suggests possible remediation actions on route configurations that have violations\.  
**Example – Route management violation and remediation suggestions**  

     A subnet is expected to send traffic through the firewall endpoints, but the current subnet is sending traffic directly to the internet gateway\. This is a route management violation\. The suggested remediation in this case might be a list of ordered actions\. The first being a recommendation to add the required routes to the Network Firewall subnet's route table to direct outgoing traffic to the internet gateway and to direct incoming traffic for destinations inside the VPC to ``local``\. The second recommendation is to replace the internet gateway route or the invalid Network Firewall route in the subnet's route table to direct outgoing traffic to the firewall endpoints\. The third recommendation is to add required routes to the internet gateway's route table to direct incoming traffic to the firewall endpoints\. 
   + **`AWS::EC2:InternetGateway`** – This is used for Network Firewall policies that have Monitor mode enabled\.
     + **Route management violations** – The internet gateway is noncompliant if the internet gateway is not associated with a route table, or if there is an invalid route in the internet gateway route table\.
     + **Remediation actions for route management violations** – Firewall Manager suggests possible remediation actions to remedy route management violations\.   
**Example 1 – Route management violation and remediation suggestions**  

     An internet gateway is not associated with a route table\. The suggested remediation actions might be a list of ordered actions\. The first action is to create a route table\. The second action is to associate the route table with the internet gateway\. The third action is to add the required route to the internet gateway route table\.   
**Example 2 – Route management violation and remediation suggestions**  

     The internet gateway is associated with a valid route table, but the route is configured improperly\. The suggested remediation might be a list of ordered actions\. The first suggestion is to remove the invalid route\. The second is to add the required route to the internet gateway route table\. 
   + **`AWS::NetworkFirewall::FirewallPolicy`** – This is used for Network Firewall policies\. Firewall Manager displays information about a Network Firewall firewall policy that's been modified in a way that makes it noncompliant\. The information provides the expected firewall policy and the policy that it found in the customer account, so you can compare stateless and stateful rule groups names and priority settings, custom action names, and default stateless actions settings\. The violation description component contains a description of the expected state of the resource, the current, noncompliant state, and if available, a description of what caused the discrepancy\. 
   + **`AWS::EC2::VPC`** – This is used for DNS Firewall policies\. Firewall Manager displays information about a VPC that's in scope of a Firewall Manager DNS Firewall policy, and that is noncompliant with the policy\. The information provided includes the expected rule groups that are expected to be associated with the VPC and the actual rule groups\. The violation description component contains a description of the expected state of the resource, the current, noncompliant state, and if available, a description of what caused the discrepancy\.