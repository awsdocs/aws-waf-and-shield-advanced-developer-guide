# Responding to DDoS attacks<a name="ddos-responding"></a>

AWS automatically addresses layer 3 and layer 4 DDoS attacks\. If you use Shield Advanced to protect your Amazon EC2 instances, during an attack Shield Advanced automatically deploys your Amazon VPC network ACLs to the border of the AWS network\. This allows Shield Advanced to provide protection against larger DDoS events\. For more information about network ACLs, see [Network ACLs](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_ACLs.html)\.

If DDoS alarms in CloudWatch indicate a possible layer 7 attack, you have the following options:
+ Investigate and mitigate the attack on your own\. If you determine that the activity represents a DDoS attack, you can create your own AWS WAF rules to mitigate the attack\. AWS WAF is included with AWS Shield Advanced at no additional cost\. AWS provides preconfigured templates to get you started quickly\. The templates include a set of AWS WAF rules, which are designed to block common web\-based attacks\. You can customize the rules to fit your business needs\. For more information, see [AWS WAF Security Automations](https://aws.amazon.com/solutions/aws-waf-security-automations/) and [Creating a web ACL](web-acl-creating.md)\. 

  If you use AWS Firewall Manager, you can add these rules to a Firewall Manager AWS WAF policy\.
+ If you're an AWS Shield Advanced customer, you also have the option of contacting the [AWS Support Center](https://console.aws.amazon.com/support/home#/) to get help with mitigations\. Critical and urgent cases are routed directly to DDoS experts\. With AWS Shield Advanced, complex cases can be escalated to the AWS DDoS Response Team \(DRT\), which has deep experience in protecting AWS, Amazon\.com, and its subsidiaries\. For more information about the DRT, see [The AWS DDoS Response Team \(DRT\)](ddos-overview.md#ddos-drt)\.

  To get DDoS Response Team \(DRT\) support, contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\. Select the following options:
  + Case type: Technical Support
  + Service: Distributed Denial of Service \(DDoS\)
  + Category: Inbound to AWS
  + Severity: *Choose an appropriate option*

  When discussing with our representative, explain that you're an AWS Shield Advanced customer experiencing a possible DDoS attack\. Our representative will direct your call to the appropriate DDoS experts\. If you open a case with the [AWS Support Center](https://console.aws.amazon.com/support/home#/) using the **Distributed Denial of Service \(DDoS\)** service type, you can speak directly with a DDoS expert by chat or telephone\. DDoS support engineers can help you identify attacks, recommend improvements to your AWS architecture, and provide guidance in the use of AWS services for DDoS attack mitigation\.
**Important**  
For layer 7 attacks, the DRT can help you analyze the suspicious activity, and then assist you to mitigate the issue\. This mitigation often requires the DRT to create or update AWS WAF web access control lists \(web ACLs\) in your account\. However, they need your permission to do so\. We recommend that as part of enabling AWS Shield Advanced, you follow the steps in [Step 5: Configure AWS DRT support](authorize-DRT.md) to proactively provide the DRT with the needed permissions\. Providing permission ahead of time helps to prevent any delays in the event of an actual attack\.

  You can also contact the DRT before or during a possible attack to develop and deploy custom mitigations\. For example, if you're running a web application and need only ports 80 and 443 open, you can work with the DRT to preconfigure a web ACL to "allow" only ports 80 and 443\.

  You authorize and contact the DRT at the account level\. That is, if you use Shield Advanced within a Firewall Manager Shield Advanced policy, the account owner, not the Firewall Manager administrator, must contact the DRT for support\. The Firewall Manager administrator can contact the DRT only for accounts that they own\.