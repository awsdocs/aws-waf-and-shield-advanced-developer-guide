# AWS Shield Advanced event summaries<a name="ddos-event-summaries"></a>

You can view summary and detail information for an event in the event's console page\. To open the page for an event, select its AWS resource name from the **Events** page list\. 

The following screenshot shows an example event summary for a network layer event\. 

![\[The summary pane of the AWS Shield console event page lists information for an event and includes the affected AWS resource, attack vectors, start and end times, and mitigation and status information.\]](http://docs.aws.amazon.com/waf/latest/developerguide/)

The event page summary information includes the following\. 
+ **Current status** – Values that indicate the state of the event and the actions that Shield Advanced has taken on the event\. Status values apply to infrastructure layer \(layer 3 or 4\) and application layer \(layer 7\) events\. 
  + **Identified \(ongoing\)** and **Identified \(subsided\)** – These indicate that Shield Advanced detected an event, but has taken no action on it so far\. **Identified \(subsided\)** indicates that the suspicious traffic that Shield detected has stopped without intervention\. 
  + **Mitigation in progress** and **Mitigated** – These indicate that Shield Advanced detected an event and has taken action on it\. **Mitigated** is also used when the targeted resource is an Amazon CloudFront distribution or Amazon Route 53 hosted zone, which have their own automatic inline mitigations\.
+ **Attack vectors** – DDoS attack vectors like TCP SYN floods and Shield Advanced detection heuristics like request flood\. These can be indicators of a DDoS attack\. 
+ **Start time** – The date and time that the first anomalous traffic data point was detected\. 
+ **Duration or end time** – Indicates the time elapsed between the event start time and the last observed anomalous data point that Shield Advanced observed\. While an event is ongoing, these values will continue to increase\.
+ **Protection** – Names the Shield Advanced protection that's in associated with the resource, and provides a link to its protection page\. This is available in the individual event's page\.
+ **Automatic application layer DDoS mitigation** – Used for application layer protections, to indicate whether the Shield Advanced automatic application layer DDoS mitigation is enabled for the resource\. If it is enabled, this provides a link to access and manage the configuration\. This is available in the individual event's page\.
+ **Network layer automatic mitigation** – Indicates whether the resource has automatic mitigation at the network layer\. If a resource has a network layer component, it will have this enabled\. This information is available in the individual event's page\.

For resources that are frequently targeted, Shield may leave mitigations in place after excess traffic has subsided, to prevent further recurring events\. 

**Note**  
You can also access event summaries for protected resources through the AWS Shield API operation [ListAttacks](https://docs.aws.amazon.com/waf/latest/DDOSAPIReference/API_ListAttacks.html)\.