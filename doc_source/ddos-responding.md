# Responding to DDoS events<a name="ddos-responding"></a>

AWS automatically mitigates network and transport layer \(layer 3 and layer 4\) Distributed Denial of Service \(DDoS\) attacks\. If you use Shield Advanced to protect your Amazon EC2 instances, during an attack Shield Advanced automatically deploys your Amazon VPC network ACLs to the border of the AWS network\. This allows Shield Advanced to provide protection against larger DDoS events\. For more information about network ACLs, see [Network ACLs](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_ACLs.html)\.

For application layer \(layer 7\) DDoS attacks, AWS attempts to detect and notify AWS Shield Advanced customers through CloudWatch alarms\. By default, it doesn't automatically apply mitigations, to avoid inadvertently blocking valid user traffic\. 

For application layer \(layer 7\) resources, you have the following options available for responding to an attack\. 
+ **Provide your own mitigations** – You can investigate and mitigate the attack on your own\. For information, see [Manually mitigating an application layer DDoS attack](#ddos-responding-manual)\. 
+ **Contact support** – If you're a Shield Advanced customer, you can contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/) to get help with mitigations\. Critical and urgent cases are routed directly to DDoS experts\. For information, see [Contacting the support center during an application layer DDoS attack](#ddos-responding-contact-support)\. 

Additionally, before an attack occurs, you can proactively enable the following mitigation options: 
+ **Automatic mitigations on Amazon CloudFront distributions** – With this option, Shield Advanced defines and manages mitigating rules for you in your web ACL\. For information about automatic application layer mitigation, see [Shield Advanced automatic application layer DDoS mitigation](ddos-automatic-app-layer-response.md)\. 
+ **Proactive engagement** – When AWS Shield Advanced detects a large application layer attack against one of your applications, the SRT can proactively contact you\. The SRT triages the DDoS event and creates AWS WAF mitigations\. The SRT contacts you and, with your consent, can apply the AWS WAF rules\. For more information about this option, see [Configuring proactive engagement](ddos-srt-proactive-engagement.md)\.

## Contacting the support center during an application layer DDoS attack<a name="ddos-responding-contact-support"></a>

If you're an AWS Shield Advanced customer, you can contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/) to get help with mitigations\. Critical and urgent cases are routed directly to DDoS experts\. With AWS Shield Advanced, complex cases can be escalated to the AWS Shield Response Team \(SRT\), which has deep experience in protecting AWS, Amazon\.com, and its subsidiaries\. For more information about the SRT, see [Shield Response Team \(SRT\) support](ddos-srt-support.md)\.

To get Shield Response Team \(SRT\) support, contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\. The response time for your case depends on the severity that you select and the response times, which are documented on the [AWS Support Plans](https://aws.amazon.com/premiumsupport/compare-plans/) page\.

Select the following options:
+ Case type: Technical Support
+ Service: Distributed Denial of Service \(DDoS\)
+ Category: Inbound to AWS
+ Severity: *Choose an appropriate option*

When discussing with our representative, explain that you're an AWS Shield Advanced customer experiencing a possible DDoS attack\. Our representative will direct your call to the appropriate DDoS experts\. If you open a case with the [AWS Support Center](https://console.aws.amazon.com/support/home#/) using the **Distributed Denial of Service \(DDoS\)** service type, you can speak directly with a DDoS expert by chat or telephone\. DDoS support engineers can help you identify attacks, recommend improvements to your AWS architecture, and provide guidance in the use of AWS services for DDoS attack mitigation\.

For application layer attacks, the SRT can help you analyze the suspicious activity\. If you have automatic mitigation enabled for your resource, the SRT can review the mitigations that Shield Advanced is automatically placing against the attack\. In any case, the SRT can assist you to review and mitigate the issue\. Mitigations that the SRT recommends often require the SRT to create or update AWS WAF web access control lists \(web ACLs\) in your account\. The SRT will need your permission to do this work\. 

**Important**  
We recommend that as part of enabling AWS Shield Advanced, you follow the steps in [Configuring access for the Shield Response Team \(SRT\)](ddos-srt-access.md) to proactively provide the SRT with the permissions that they need to assist you during an attack\. Providing permission ahead of time helps to prevent any delays in the event of an actual attack\.

The SRT helps you triage the DDoS attack to identify attack signatures and patterns\. With your consent, the SRT creates and deploys AWS WAF rules to mitigate the attack\.

You can also contact the SRT before or during a possible attack to review mitigations and to develop and deploy custom mitigations\. For example, if you're running a web application and need only ports 80 and 443 open, you can work with the SRT to preconfigure a web ACL to "allow" only ports 80 and 443\.

You authorize and contact the SRT at the account level\. That is, if you use Shield Advanced within a Firewall Manager Shield Advanced policy, the account owner, not the Firewall Manager administrator, must contact the SRT for support\. The Firewall Manager administrator can contact the SRT only for accounts that they own\.

## Manually mitigating an application layer DDoS attack<a name="ddos-responding-manual"></a>

If you determine that the activity in the events page for your resource represents a DDoS attack, you can create your own AWS WAF rules in your web ACL to mitigate the attack\. This is the only option available if you aren't a Shield Advanced customer\. AWS WAF is included with AWS Shield Advanced at no additional cost\. For information about creating rules in your web ACL, see [Web access control lists \(web ACLs\)](web-acl.md)\.

If you use AWS Firewall Manager, you can add your AWS WAF rules to a Firewall Manager AWS WAF policy\.

**To manually mitigate a potential application layer DDoS attack**

1. Create rule statements in your web ACL with criteria that matches the unusual behavior\. To start with, configure them to count matching requests\. For information about configuring your web ACL and rule statements, see [Web ACL rule and rule group evaluation](web-acl-processing.md) and [Testing and tuning your AWS WAF protections](web-acl-testing.md)\.
**Note**  
Always test your rules first by initially using the rule action `Count` instead of `Block`\. After you're comfortable that your new rules are identifying the correct requests, you can modify them to block the requests\. 

1. Monitor the request counts to determine whether you want to block the matching requests\. If the volume of requests continues to be unusually high and you're confident that your rules are capturing the requests that are causing the high volume, change the rules in your web ACL to block the requests\. 

1. Continue monitoring the events page to ensure that your traffic is being handled as you want it to be\. 

AWS provides preconfigured templates to get you started quickly\. The templates include a set of AWS WAF rules that you can customize and use to block common web\-based attacks\. For more information, see [AWS WAF Security Automations](https://aws.amazon.com/solutions/aws-waf-security-automations/)\.