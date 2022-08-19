# AWS Shield Advanced event details<a name="ddos-event-details"></a>

You can see details about an event's detection, mitigation, and top contributors in the bottom section of the console page for the event\. This section can include a mix of legitimate and potentially unwanted traffic, and may represent both traffic that was passed to your protected resource and traffic that was blocked by Shield mitigations\.
+ **Detection and mitigation** – Provides information about the observed event and any applied mitigations against it\. For information about event mitigation, see [Responding to DDoS events](ddos-responding.md)\.
+ **Top contributors** – Categorizes the traffic that's involved in the event, and lists the primary sources of traffic for each category\. 

Mitigation metrics aren't included for Amazon CloudFront or Amazon Route 53 resources, because these services are protected by a mitigation system that's always enabled and doesn't require mitigations for individual resources\. 

The details sections vary according to whether the information is for an infrastructure layer or application layer event\. 

## Application layer event details<a name="ddos-event-details-application-layer"></a>

For an application layer \(layer 7\) event, the **Detection and mitigation** tab shows detection metrics that are based on information obtained from the AWS WAF logs\. Mitigation metrics are based on AWS WAF rules in the associated web ACL that are configured to block the unwanted traffic\. Event traffic that subsides before a mitigating rule takes effect isn't represented in the mitigation metrics\. This can result in a difference between the web request traffic shown in the detection graphs and the allow and block metrics shown in the mitigation graphs\. 

With application layer resources, you can choose to define your own mitigating rules in your web ACL, you can request help from the Shield Response Team \(SRT\), or for Amazon CloudFront distributions, you can configure Shield Advanced to apply automatic mitigations\. For information about these options, see [Responding to DDoS events](ddos-responding.md)\.

The **Top contributors** tab for application layer events displays the top 5 contributors to the event, categorized by dimensions such as source IP, source country, and destination URL\.

Contributor information is based on requests for both legitimate and potentially unwanted traffic\. Larger volume events and events where the request sources aren't highly distributed are more likely to have identifiable top contributors\. A significantly distributed attack could have any number of sources, making it hard to identify top contributors to the attack\. If Shield Advanced doesn't identify significant contributors for a specific category, it displays the data as unavailable\. 

## Infrastructure layer event details<a name="ddos-event-details-infrastructure-layer"></a>

For an infrastructure layer \(layer 3 or 4\) event, the **Detection and mitigation** tab shows detection metrics that are based on sampled network flows and mitigation metrics that are based on traffic observed by the mitigation systems\. Mitigation metrics are a more precise measurement of the traffic into your resource\. 

Event traffic that subsides before Shield places a mitigation isn't represented in the mitigation metrics\. This can result in a difference between the traffic shown in the detection graphs and the pass and drop metrics shown in the mitigation graphs\. 

Shield automatically creates a mitigation for the protected resource types Elastic IP \(EIP\), Classic Load Balancer \(CLB\), Application Load Balancer \(ALB\), and AWS Global Accelerator standard accelerator\. Mitigation metrics for EIP addresses and AWS Global Accelerator standard accelerators indicate the number of passed and dropped packets\. 

The **Top contributors** tab for infrastructure layer events lists metrics for up to 100 top contributors on several traffic dimensions\. The details include network layer properties for any dimension where at least five significant sources of traffic could be identified\. Examples of sources of traffic are source IP and source ASN\. 

Contributor metrics are based on sampled network flows for both legitimate and potentially unwanted traffic\. Larger volume events and events where the traffic sources aren't highly distributed are more likely to have identifiable top contributors\. A significantly distributed attack could have any number of sources, making it hard to identify top contributors to the attack\. If Shield doesn't identify any significant contributors for a specific metric or category, it displays the data as unavailable\. 

In an infrastructure layer DDoS attack, traffic sources might be spoofed or reflected\. A spoofed source is intentionally forged by the attacker\. A reflected source is the real source of detected traffic, but it's not a willing participant in the attack\. For example, an attacker might generate a large, amplified flood of traffic to a target by reflecting the attack off of services on the internet that are usually legitimate\. In this case, the source information might be valid while it's not the actual source of the attack\. These factors can limit the viability of mitigation techniques that block sources based on packet headers\.