# Reviewing DDoS events<a name="using-ddos-reports"></a>

## Monitoring threats across AWS<a name="aws-shield-global-threats"></a>

Use the AWS Shield global threat dashboard to view trends and metrics about the DDoS threat landscape across Amazon EC2, Amazon CloudFront, Elastic Load Balancing, and Amazon Route 53\.

The global threat dashboard provides a near real\-time summary of the global AWS threat landscape, including the largest event, the top event vectors, and the relative number of significant events\. You can customize the dashboard view for different time durations to see the history of significant DDoS events\.

**Note**  
The console guidance provided here is for the latest version of the AWS Shield console, released in 2020\. In the console, you can switch between versions\. <a name="review-ddos-threat-dashboard"></a>

**To view the global threat dashboard**

1. Sign in to the AWS Management Console and open the AWS WAF & Shield console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the **AWS Shield** navigation bar, choose **Global threat dashboard**\.

1. Choose a time period\.

You can use the information on the global threat dashboard to better understand the threat landscape and help you make decisions to better protect your AWS resources\.

## Shield Advanced metrics and reports<a name="shield-details"></a>

AWS Shield Advanced provides real\-time metrics and reports for extensive visibility into events on your AWS resources\.

These metrics and reports are available only for AWS Shield Advanced customers\. To activate AWS Shield Advanced, see [To subscribe to AWS Shield Advanced](enable-ddos-prem.md#enable-ddos-prem-procedure)\.

You can view near real\-time metrics about events, including the following:
+ Event type
+ Start time
+ Duration
+ Blocked bits or packets per second
+ Passed bits or packets per second
+ Source and destination IP addresses
+ Protocol
+ Resource ASN
+ TCP flag

Details are available for active events and for past events that have occurred in the last 12 months\.

Additionally, AWS Shield Advanced gives you insight into your overall traffic at the time of an event\. You can review details about the most prevalent:
+ IP addresses
+ URLs
+ Referrers
+ ASNs
+ Countries
+ User Agents

Use this information to create AWS WAF rules to help prevent future attacks\. For example, if you see that you have a lot of requests coming from a country that you don't typically do business in, you can create an AWS WAF rule to block requests from that country\. 

In addition to the metrics and reports described here, you can see a year's summary of events for all of your resources, regardless of their protection status, in the **Overview** page under **Events summary in past year**\. 

**Note**  
The console guidance provided here is for the latest version of the AWS Shield console, released in 2020\. In the console, you can switch between versions\. <a name="review-ddos-reports-procedure"></a>

**To review DDoS events**

1. Sign in to the AWS Management Console and open the AWS WAF & Shield console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the **AWS Shield** navigation bar, choose **Events**\.

The **Events** page provides the following possible current status for events:

**Mitigation in progress**  
Indicates a possible layer 3 or 4 event has been identified and AWS is attempting to address the issue\.

**Mitigated**  
Indicates a possible layer 3 or 4 event was identified\. AWS responded to the event and it appears to be over\.

**Identified \(ongoing\)**  
Indicates a possible layer 7 event has been identified\. AWS cannot address layer 7 events, so you must design your own layer mitigation processes\. For more information on responding to possible layer 7 events, see [Responding to DDoS events](ddos-responding.md)\.

**Identified \(subsided\)**  
Indicates a possible layer 7 event was identified and appears to be over\.

If you determine a possible event is underway, you can contact the DDoS Response Team \(DRT\) through the [AWS Support Center](https://console.aws.amazon.com/support/home#/), or attempt to mitigate the event on your own by creating a new web access control list \(web ACL\)\. 

The **Events** page also contains tabs with additional details for detection and mitigation of events and for top contributors during an event\. 

**Detection and mitigation**  
The **Detection and mitigation** tab displays graphs that show the traffic that AWS Shield evaluated prior to reporting this event and the effect of any mitigation that was placed\. It also provides metrics for infrastructure\-layer Distributed Denial of Service \(DDoS\) events for resources in your own Amazon Virtual Private Cloud VPC and AWS Global Accelerator accelerators\. Detection and mitigation metrics are not included for Amazon CloudFront or Amazon Route 53 resources\.

AWS Shield evaluates traffic to your protected resource along multiple dimensions\. When an anomaly is detected, Shield creates an event and reports the traffic dimension where the anomaly was observed\. If the protected resource is an Elastic IP address, Classic Load Balancer \(CLB\), Application Load Balancer, or Global Accelerator accelerator, Shield automatically creates a mitigation for the protected resource\. This protects your resource from receiving excess traffic and from receiving traffic that matches a known DDoS event signature\. 

You might notice a difference between the traffic volume shown in the detection graphs and the pass and drop metrics reported on the mitigation graphs\. If the traffic that resulted in an event subsides before a mitigation is created, this traffic doesn’t appear in mitigation metrics\. The time difference between the first data point in detection metrics and the first data point in mitigation metrics is the latency between detection and mitigation of an event\. Detection metrics are based on sampled network flows while mitigation metrics are based on traffic that's observed by the mitigation systems\. Mitigation metrics are a more precise measurement of the traffic into your resource\. The DRT might leave a mitigation in place after the excess traffic has subsided\. Shield might maintain long\-running mitigations on resources that are frequently targeted\.

**Top contributors**  
The **Top contributors** tab provides insight into where traffic is coming from during a detected event\. You can view the highest volume contributors, sorted by aspects such as protocol, source port, and TCP flags\. You can download the information and you can adjust the units used and the number of contributors to display\.

Top contributors provide additional metric dimensions that you can use to understand the network traffic that’s sent to your resource during an event\. These metrics are based on sampled network flows for both legitimate and potentially unwanted traffic\. Some or all of the traffic that you see in the metrics might have been passed to your resource or blocked by Shield\. 

Top contributor data might be unavailable for a metric if no significant contributors can be identified\. Events that are more likely to have metrics with top contributors are large volume events and events where the traffic sources aren't highly distributed\. 

Keep in mind that source attributes like source IP address and source ASN might be spoofed or reflected\. Spoofed packets are common in DDoS events where an attacker wants to obfuscate the real source of the traffic\. Reflected packets are common in DDoS events where an attacker wants to generate a larger, amplified flood of traffic to a target by reflecting the attack of services on the Internet that are usually legitimate\. In these cases, the source IP address or source ASN are valid, but they are not the actual source of the attack\.<a name="mitigating-ddos-attack-procedure"></a>

**To mitigate a potential DDoS attack**

1. Create conditions in AWS WAF that match the unusual behavior\.

1. Add those conditions to one or more AWS WAF rules\.

1. Add those rules to a web ACL and configure the web ACL to count the requests that match the rules\.
**Note**  
You should always test your rules first by initially using `Count` rather than `Block`\. After you're comfortable that the new rule is identifying the correct requests, you can modify your rule to block those requests\.

1. Monitor those counts to determine if the source of the requests should be blocked\. If the volume of requests continues to be unusually high, change your web ACL to block those requests\.

   For more information, see [Creating a web ACL](web-acl-creating.md)\.

AWS provides preconfigured templates to get you started quickly\. The templates include a set of AWS WAF rules that you can customize and use to block common web\-based attacks\. For more information, see [AWS WAF Security Automations](https://aws.amazon.com/solutions/aws-waf-security-automations/)\.