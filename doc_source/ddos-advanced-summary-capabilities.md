# AWS Shield Advanced capabilities and options<a name="ddos-advanced-summary-capabilities"></a>

AWS Shield Advanced subscription includes the following capabilities and options\. These supplement the DDoS detection and mitigation capabilities that you already receive with AWS\. 
+ **AWS WAF integration** – Shield Advanced uses AWS WAF web ACLs, rules, and rule groups as part of its application layer protections\. Your subscription to Shield Advanced covers the basic AWS WAF fees for web ACLs, rules, and web requests\. 

  For more information about AWS WAF, see [How AWS WAF works](how-aws-waf-works.md)\. For information about the basic AWS WAF costs, see [AWS WAF Pricing](http://aws.amazon.com/waf/pricing/)\. Your subscription to Shield Advanced does not cover any additional AWS WAF costs, such as those for the optional intelligent threat mitigation capabilities of Bot Control or `CAPTCHA`\. For information about Shield Advanced pricing, see [AWS Shield Advanced Pricing](http://aws.amazon.com/shield/pricing/)\.
+ **Automatic application layer DDoS mitigation** – You can configure Shield Advanced to respond automatically to mitigate application layer \(layer 7\) attacks against your protected resources\. With automatic mitigation, Shield Advanced responds to a detected DDoS attack by creating, evaluating, and deploying custom AWS WAF rules for your protected resource\. You can configure automatic mitigation to count or block the web requests that are part of an attack\. 

  For more information, see [Shield Advanced automatic application layer DDoS mitigation](ddos-automatic-app-layer-response.md)\.
+ **Health\-based detection** – You can use Amazon Route 53 health checks with Shield Advanced to inform event detection and mitigation\. Health checks monitor your application according to your specifications, reporting healthy when your specifications are met and unhealthy when they aren't\. Using health checks with Shield Advanced helps prevent false positives and provides faster detection and mitigation when a protected resource is unhealthy\. You can use health\-based detection for any resource type except Route 53 hosted zones\. Shield Advanced proactive engagement is available only for resources that have health\-based detection enabled\. 

  For more information, see [Configuring health\-based detection using health checks](ddos-advanced-health-checks.md)\.
+ **Protection groups** – You can use protection groups to create logical groupings of your protected resources, for enhanced detection and mitigation of the group as a whole\. You can define the criteria for membership in a protection group so that newly protected resources are automatically included\. A protected resource can belong to multiple protection groups\. 

  For more information, see [AWS Shield Advanced protection groups](ddos-protection-groups.md)\.
+ **Enhanced visibility into DDoS events and attacks** – Shield Advanced gives you access to advanced, real\-time metrics and reports for extensive visibility into events and attacks on your protected AWS resources\. You can access this information through the Shield Advanced API and console, and through Amazon CloudWatch metrics\. 

  For more information, see [Visibility into DDoS events](ddos-viewing-events.md)\.
+ **Centralized management of Shield Advanced protections by AWS Firewall Manager** – You can use Firewall Manager to automatically apply Shield Advanced protections to your new accounts and resources and to deploy AWS WAF rules to your web ACLs\. Firewall Manager Shield Advanced protection policies are included at no additional charge for Shield Advanced customers\. You can also centralize your Shield Advanced monitoring activities for your accounts by using Firewall Manager with an Amazon Simple Notification Service \(SNS\) topic or AWS Security Hub\. 

  For more information about using Firewall Manager with Shield Advanced, see [AWS Firewall Manager](fms-chapter.md) and [AWS Shield Advanced policies](shield-policies.md)\. For information about Firewall Manager pricing, see [AWS Firewall Manager Pricing](http://aws.amazon.com/firewall-manager/pricing/)\.
+ **AWS Shield Response Team \(SRT\)** – The SRT has deep experience in protecting AWS, Amazon\.com, and its subsidiaries\. As an AWS Shield Advanced customer, you can contact the SRT at any time for assistance during a DDoS attack that affects the availability of your application\. You can also work with the SRT to create and manage custom mitigations for your resources\. To use the services of the SRT, you must also be subscribed to the [Business Support plan](https://aws.amazon.com/premiumsupport/business-support/) or the [Enterprise Support plan](https://aws.amazon.com/premiumsupport/enterprise-support/)\.

  For more information, see [Shield Response Team \(SRT\) support](ddos-srt-support.md)\.
+ **Proactive engagement** – With proactive engagement, the Shield Response Team \(SRT\) contacts you directly if the Amazon Route 53 health check that you have associated with your protected resource becomes unhealthy during an event that's detected by Shield Advanced\. This allows you to engage with experts more quickly when the availability of your application might be affected by a suspected attack\. 

  For more information, see [Configuring proactive engagement](ddos-srt-proactive-engagement.md)\.
+ **Cost protection opportunities** – Shield Advanced offers some cost protection against spikes in your AWS bill that might result from a DDoS attack against your protected resources\. 

  For more information, see [Requesting a credit in AWS Shield Advanced](request-refund.md)\. 