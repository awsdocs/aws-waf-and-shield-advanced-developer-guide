# The AWS Shield Response Team \(SRT\)<a name="ddos-drt"></a>

With AWS Shield Advanced, complex DDoS events can be escalated to the AWS Shield Response Team \(SRT\), which has deep experience in protecting AWS, Amazon\.com, and its subsidiaries\.

For network and transport layer \(layer 3 and layer 4\) attacks, AWS provides automatic attack detection and proactively applies mitigations on your behalf\. For application layer \(layer 7\) DDoS attacks, AWS attempts to detect and notify AWS Shield Advanced customers through CloudWatch alarms, but only automatically applies mitigations if those are enabled for the resource\. This is to avoid inadvertently dropping valid user traffic\. 

The options for mitigating application layer attacks use AWS WAF web ACLs\. AWS WAF is included with AWS Shield Advanced at no extra cost\. 

AWS Shield Advanced customers have the following options to mitigate application layer attacks\. 
+ **Enable automatic mitigations** – With this option, Shield Advanced defines mitigating rules for you in your web ACL\. For information about automatic application layer mitigation, see [Shield Advanced automatic application layer DDoS mitigation](ddos-advanced-automatic-app-layer-response.md)\. 
+ **Provide your own mitigations** – You can create your own AWS WAF rules to mitigate the DDoS attacks\. AWS provides preconfigured templates to get you started quickly\. The templates include a set of AWS WAF rules that are designed to block common web\-based attacks\. You can customize the templates to fit your business needs\. For more information, see [AWS WAF Security Automations](https://aws.amazon.com/solutions/aws-waf-security-automations/)\.
+ **Engage the SRT** – If you want additional support in preventing attacks or addressing an attack, you can contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\. Critical and urgent cases are routed directly to DDoS experts\. With AWS Shield Advanced, complex cases can be escalated to the SRT, which has deep experience in protecting AWS, Amazon\.com, and its subsidiaries\. If you are an AWS Shield Advanced customer, you also can request special handling instructions for high severity cases\.

  The response time for your case depends on the severity that you select and the response times, which are documented on the [AWS Support Plans](https://aws.amazon.com/premiumsupport/compare-plans/) page\.

  The SRT helps you triage the DDoS attack to identify attack signatures and patterns\. With your consent, the SRT creates and deploys AWS WAF rules to mitigate the attack\.

When AWS Shield Advanced detects a large application layer attack against one of your applications, the SRT might proactively contact you\. The SRT triages the DDoS event and creates AWS WAF mitigations\. The SRT then contacts you for consent to apply the AWS WAF rules\. 