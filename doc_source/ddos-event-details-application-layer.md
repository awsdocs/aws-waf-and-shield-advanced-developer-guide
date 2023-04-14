# Application layer event details<a name="ddos-event-details-application-layer"></a>

For an application layer \(layer 7\) event, the **Detection and mitigation** tab shows detection metrics that are based on information obtained from the AWS WAF logs\. Mitigation metrics are based on AWS WAF rules in the associated web ACL that are configured to block the unwanted traffic\. 

The following screenshot shows an example of the detection metrics for an application layer event that subsided after a number of hours\. 

![\[A detection metrics graph shows detection of request flood traffic from 11:30 until it subsides at 16:00.\]](http://docs.aws.amazon.com/waf/latest/developerguide/)

Event traffic that subsides before a mitigating rule takes effect isn't represented in mitigation metrics\. This can result in a difference between the web request traffic shown in the detection graphs and the allow and block metrics shown in the mitigation graphs\. 

For Amazon CloudFront distributions, you can configure Shield Advanced to apply automatic mitigations for you\. With any application layer resources, you can choose to define your own mitigating rules in your web ACL and you can request help from the Shield Response Team \(SRT\)\. For information about these options, see [Responding to DDoS events](ddos-responding.md)\.

The **Top contributors** tab for application layer events displays the top 5 contributors to the event, categorized by dimensions such as source IP, source country, and destination URL\.

The following screenshot shows an example **Top contributors** tab for an application layer event\. 

![\[The top contributors tab for an application layer event describes the top 5 contributors for a number of web request characteristics. The screen shows the top 5 source IP addresses, top 5 destination URLs, top 5 source countries, and top 5 user agents.\]](http://docs.aws.amazon.com/waf/latest/developerguide/)

Contributor information is based on requests for both legitimate and potentially unwanted traffic\. Larger volume events and events where the request sources aren't highly distributed are more likely to have identifiable top contributors\. A significantly distributed attack could have any number of sources, making it hard to identify top contributors to the attack\. If Shield Advanced doesn't identify significant contributors for a specific category, it displays the data as unavailable\. 