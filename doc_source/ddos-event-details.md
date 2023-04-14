# AWS Shield Advanced event details<a name="ddos-event-details"></a>

You can see details about an event's detection, mitigation, and top contributors in the bottom section of the console page for the event\. This section can include a mix of legitimate and potentially unwanted traffic, and may represent both traffic that was passed to your protected resource and traffic that was blocked by Shield mitigations\.
+ **Detection and mitigation** – Provides information about the observed event and any applied mitigations against it\. For information about event mitigation, see [Responding to DDoS events](ddos-responding.md)\.
+ **Top contributors** – Categorizes the traffic that's involved in the event, and lists the primary sources of traffic for each category\. 

Mitigation metrics aren't included for Amazon CloudFront or Amazon Route 53 resources, because these services are protected by a mitigation system that's always enabled and doesn't require mitigations for individual resources\. 

The details sections vary according to whether the information is for an infrastructure layer or application layer event\. 