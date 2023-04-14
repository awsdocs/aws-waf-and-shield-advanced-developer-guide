# Infrastructure layer event details<a name="ddos-event-details-infrastructure-layer"></a>

For an infrastructure layer \(layer 3 or 4\) event, the **Detection and mitigation** tab shows detection metrics that are based on sampled network flows and mitigation metrics that are based on traffic observed by the mitigation systems\. Mitigation metrics are a more precise measurement of the traffic into your resource\. 

The following screenshot shows an example **Detection and mitigation** tab for an infrastructure layer event\. 

![\[The detection and mitigation graphs for a network event show increasing SYN flood and packet flood traffic in the detection metrics, matched by a an increase in mitigations that drop traffic a few seconds later, in the mitigation metrics. After about thirty seconds of increased mitigations, the traffic floods stop.\]](http://docs.aws.amazon.com/waf/latest/developerguide/)

Event traffic that subsides before Shield places a mitigation isn't represented in the mitigation metrics\. This can result in a difference between the traffic shown in the detection graphs and the pass and drop metrics shown in the mitigation graphs\. 

Shield automatically creates a mitigation for the protected resource types Elastic IP \(EIP\), Classic Load Balancer \(CLB\), Application Load Balancer \(ALB\), and AWS Global Accelerator standard accelerator\. Mitigation metrics for EIP addresses and AWS Global Accelerator standard accelerators indicate the number of passed and dropped packets\. 

The **Top contributors** tab for infrastructure layer events lists metrics for up to 100 top contributors on several traffic dimensions\. The details include network layer properties for any dimension where at least five significant sources of traffic could be identified\. Examples of sources of traffic are source IP and source ASN\. 

The following screenshot shows an example **Top contributors** tab for an infrastructure layer event\. 

![\[The top contributors tab for a network event shows the categories of traffic that contributed the most to the event. The categories in this case include volume by protocol, volume by protocol and destination port, volume by protocol and source ASN, and volume by TCP flags.\]](http://docs.aws.amazon.com/waf/latest/developerguide/)

Contributor metrics are based on sampled network flows for both legitimate and potentially unwanted traffic\. Larger volume events and events where the traffic sources aren't highly distributed are more likely to have identifiable top contributors\. A significantly distributed attack could have any number of sources, making it hard to identify top contributors to the attack\. If Shield doesn't identify any significant contributors for a specific metric or category, it displays the data as unavailable\. 

In an infrastructure layer DDoS attack, traffic sources might be spoofed or reflected\. A spoofed source is intentionally forged by the attacker\. A reflected source is the real source of detected traffic, but it's not a willing participant in the attack\. For example, an attacker might generate a large, amplified flood of traffic to a target by reflecting the attack off of services on the internet that are usually legitimate\. In this case, the source information might be valid while it's not the actual source of the attack\. These factors can limit the viability of mitigation techniques that block sources based on packet headers\.