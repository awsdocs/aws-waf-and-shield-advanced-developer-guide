# AWS Shield Advanced event summaries<a name="ddos-event-summaries"></a>

You can see summary information for events on the resources that you have protected with Shield Advanced in the console page for the event\. 

**Note**  
You can also access event summaries for protected resources through the AWS Shield API operation [ListAttacks](https://docs.aws.amazon.com/waf/latest/DDOSAPIReference/API_ListAttacks.html)\.

AWS Shield evaluates traffic to your protected resource along multiple dimensions\. When an anomaly is detected, Shield Advanced creates an event\. An event is specific to a single resource, so if multiple resources are targeted at the same time, the **Events** page lists one event for each resource\. Shield Advanced might also automatically place mitigations against attacks, depending on the traffic type and on your configured protections\. These mitigations can protect your resource from receiving excess traffic or traffic that matches a known DDoS attack signature\.

The event summary information includes the following\. Some of this information is only available in the individual event's page\. 
+ **Current status** – Values that indicate the state of the event and the actions that Shield Advanced has taken on the event\. Status values apply to infrastructure layer \(layer 3 or 4\) and application layer \(layer 7\) events\. 
  + **Identified \(ongoing\)** and **Identified \(subsided\)** – These indicate that Shield Advanced detected an event, but has taken no action on it so far\. **Identified \(subsided\)** indicates that the suspicious traffic that Shield detected has stopped without intervention\. 
  + **Mitigation in progress** and **Mitigated** – These indicate that Shield Advanced detected an event and has taken action on it\. **Mitigated** is also used when the targeted resource is an Amazon CloudFront distribution or Amazon Route 53 hosted zone, which have their own automatic inline mitigations\.
+ **Attack vectors** – DDoS attack vectors like TCP SYN floods and Shield Advanced detection heuristics like request flood\. These can be indicators of a DDoS attack\. 
+ **Start time** – The date and time that the first anomalous traffic data point was detected\. 
+ **Duration or end time** – Indicates the time elapsed between the event start time and the last observed anomalous data point that Shield Advanced observed\. While an event is ongoing, these values will continue to increase\.
+ **Protection** – Names the Shield Advanced protection that's in associated with the resource, and provides a link to its protection page\. This is available in the individual event's page\.
+ **Automatic application layer DDoS mitigation** – Used for application layer protections, to indicate whether the Shield Advanced automatic application layer DDoS mitigation is enabled for the resource\. If it is enabled, this provides a link to access and manage the configuration\. This is available in the individual event's page\.
+ **Network layer automatic mitigation** – Indicates whether the resource has automatic mitigation at the network layer\. If a resource has a network layer component, it will have this enabled\. This information is available in the individual event's page\.

The following screenshot shows an example event summary listing in the **Events** page\. 

![\[The AWS Shield console left navigation pane has the Events selection highlighted in red, with a numeral 1 beside it, inside a red circle. The Events page is open, and shows a single row in the events list. The row lists an AWS resource of type CloudFront distribution. The Current status field contains a triangular red icon next to the words Mitigation in progress. The Attack vectors status field contains UDP traffic. The Start time field contains Sep 16th 2020, 2:43:00 pm SAST. The Duration field contains 6 minutes.\]](http://docs.aws.amazon.com/waf/latest/developerguide/)

The following screenshot shows an example event summary in the page for a single event\. 

![\[A section of the AWS Shield console event page has the following breadcrumbs at the top: Shield '>' Events '>' ID of a protected Amazon CloudFront distribution. Below the breadcrumbs is the title Event summary over a pane of information. On the left side of the pane, the following titles and information are listed: AWS resource with the Amazon Resource Name (ARN) of the Amazon CloudFront distribution; Attack vectors with UDP traffic; Start time with Jan 13th 2022, 2:06:00 am PST; End time with Jan 13th 2022, 2:11:00 am PST. On the right side of the pane, the following titles and information are listed: Protection with a protection ID of FMManagedShieldProtection followed by a resource ID; Automatic application layer DDoS mitigation with Not applicable; Network layer automatic mitigation with a green check mark followed by the word Enabled; Status with a green check mark followed by the word Mitigated.\]](http://docs.aws.amazon.com/waf/latest/developerguide/)

For resources that are frequently targeted, Shield may leave mitigations in place after excess traffic has subsided, to prevent further recurring events\. 