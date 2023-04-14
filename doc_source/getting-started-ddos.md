# Getting started with AWS Shield Advanced<a name="getting-started-ddos"></a>

This tutorial walks you through getting started with AWS Shield Advanced\. Shield Advanced provides advanced DDoS detection and mitigation protection for network layer \(layer 3\), transport layer \(layer 4\), and application layer \(layer 7\) attacks\. 

For more information about Shield Advanced, see [AWS Shield Advanced overview](ddos-advanced-summary.md)\.

**Note**  
It's important that you fully configure Shield Advanced prior to a Distributed Denial of Service \(DDoS\) event\. Complete the following steps to help ensure that your application is protected and that you are ready to respond if your application is affected by a DDoS attack\.

Perform the following steps in sequence\. 

**Contents**
+ [Subscribe to AWS Shield Advanced](enable-ddos-prem.md)
+ [Add resources to protect and configure protections](ddos-choose-resources.md)
  + [Configure application layer \(layer 7\) DDoS protections with AWS WAF](ddos-get-started-web-acl-rbr.md)
  + [Configure health\-based detection for your protections](ddos-get-started-health-checks.md)
  + [Configure alarms and notifications](ddos-get-started-create-alarms.md)
  + [Review and finish your protection configuration](ddos-get-started-review-and-configure.md)
+ [Configure AWS SRT support](authorize-srt.md)
+ [Create a DDoS dashboard in CloudWatch and set CloudWatch alarms](deploy-waf-dashboard.md)