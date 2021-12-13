# Reviewing DDoS events<a name="using-ddos-reports"></a>

## Monitoring threats across AWS<a name="aws-shield-global-threats"></a>

Use the AWS Shield global threat dashboard to view trends and metrics about the DDoS threat landscape across Amazon EC2, Amazon CloudFront, Elastic Load Balancing, and Amazon Route 53\.

The global threat dashboard provides a near real\-time summary of the global AWS threat landscape, including the largest event, the top event vectors, and the relative number of significant events\. You can customize the dashboard view for different time durations to see the history of significant DDoS events\.<a name="review-ddos-threat-dashboard"></a>

**To view the global threat dashboard**

1. Sign in to the AWS Management Console and open the AWS WAF & Shield console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the **AWS Shield** navigation bar, choose **Global threat dashboard**\.

1. Choose a time period\.

You can use the information on the global threat dashboard to better understand the threat landscape and help you make decisions to better protect your AWS resources\.

## Shield Advanced metrics and reports<a name="shield-details"></a>

AWS Shield Advanced provides real\-time metrics and reports for extensive visibility into events on your AWS resources\.

These metrics and reports are available only for Shield Advanced customers\. To activate Shield Advanced, see [To subscribe to AWS Shield Advanced](enable-ddos-prem.md#enable-ddos-prem-procedure)\.<a name="review-ddos-reports-procedure"></a>

**To review DDoS events**

1. Sign in to the AWS Management Console and open the AWS WAF & Shield console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the **AWS Shield** navigation bar, choose **Events**\.

The events page provides an overview of attacks on your protected resources, including status and timing information\. 

You can select any resource to get more details about a specific attack\. 

**Events summary**  
The events summary page for a resource provides more detail about an attack, including start and end time, the protections that you have enabled for the resource, and any mitigation activities that have been or are being applied for the attack\. 

From this page, you can choose to modify your automatic application layer DDoS mitigation configuration for the resource\. For information about this option, see [Shield Advanced automatic application layer DDoS mitigation](ddos-advanced-automatic-app-layer-response.md)\. 

This page provides tabs for **Detection and mitigation** and for the **Top contributors** that have been identified for the attack\. The details that are provided in these tabs depend on whether they are for an application layer or network layer attack\. 

**Detection and mitigation**  
The **Detection and mitigation** tab displays graphs that show the traffic that AWS Shield evaluated prior to reporting this event and the effect of any mitigation that was placed\. It also provides metrics for infrastructure\-layer DDoS events for resources in your own Amazon Virtual Private Cloud VPC and AWS Global Accelerator accelerators\. Network layer detection and mitigation metrics are not included for Amazon CloudFront or Amazon Route 53 resources\.

AWS Shield evaluates traffic to your protected resource along multiple dimensions\. When an anomaly is detected, Shield creates an event and reports the traffic dimension where the anomaly was observed\. For network layer attacks, if the protected resource is an Elastic IP address, Classic Load Balancer, Application Load Balancer, or Global Accelerator accelerator, Shield automatically creates a mitigation for the protected resource\. 

For application layer attacks on Amazon CloudFront distributions, if the resource has automatic application layer DDoS mitigation enabled, Shield Advanced automatically creates a mitigation for the protected resource according to your configuration\. These mitigations protect your resource from receiving excess traffic and from receiving traffic that matches a known DDoS event signature\. If you have enabled automatic application layer DDoS mitigation in `Block` mode, you can see metrics for requests that are being blocked by the rule group that Shield Advanced manages in your web ACL\. If you use `Count` mode and need information about counted requests, contact the support center, as described at [Contacting the support center during an application layer DDoS attack](ddos-responding.md#ddos-responding-contact-support)\. For information about automatic mitigation, see [Shield Advanced automatic application layer DDoS mitigation](ddos-advanced-automatic-app-layer-response.md)\.

For network layer attacks, you might notice a difference between the traffic volume shown in the detection graphs and the pass and drop metrics reported on the mitigation graphs\. If the traffic that resulted in an event subsides before a mitigation is created, this traffic doesn’t appear in mitigation metrics\. The time difference between the first data point in detection metrics and the first data point in mitigation metrics is the latency between detection and mitigation of an event\. Detection metrics are based on sampled network flows while mitigation metrics are based on traffic that's observed by the mitigation systems\. Mitigation metrics are a more precise measurement of the traffic into your resource\. The SRT might leave a mitigation in place after the excess traffic has subsided\. Shield might maintain long\-running mitigations on resources that are frequently targeted\.

**Top contributors**  
The **Top contributors** tab provides insight into the nature of the highest volume of traffic\. For network layer attacks, the top contributors are sorted by aspects such as protocol, source port, and TCP flags\. For application layer attacks, the top contributors are sorted by aspects such as source IP address, source country, and destination URLs\. 

Top contributors provide additional dimensions that you can use to understand the traffic that’s sent to your resource during an event\. This information is for both legitimate and potentially unwanted traffic\. Some or all of the traffic that you see for top contributors might have been passed to your resource or blocked by Shield\. 

Top contributor data might be unavailable in some categories if no significant contributors can be identified\. Events that are more likely to have top contributors are large volume events and events where the traffic sources aren't highly distributed\. 

Keep in mind that source attributes like source IP address and source ASN might be spoofed or reflected\. Spoofed packets are common in DDoS events where an attacker wants to obfuscate the real source of the traffic\. Reflected packets are common in network layer DDoS events where an attacker wants to generate a larger, amplified flood of traffic to a target by reflecting the attack of services on the internet that are usually legitimate\. In these cases, the source IP address or source ASN are valid, but they are not the actual source of the attack\.