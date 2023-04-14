# AWS Shield Advanced events<a name="ddos-events"></a>

When you subscribe to Shield Advanced, and protect your resources, you gain access to additional visibility features for the resources\. These include near real\-time notification of events that are detected by Shield Advanced and additional information about detected events and mitigations\. 

AWS Shield evaluates traffic to your protected resource along multiple dimensions\. When an anomaly is detected, Shield Advanced creates a separate event for each resource that's affected\. 

You can access event summaries and details through the **Events** page of the Shield console\. The top level **Events** page provides an overview of current and past events\. 

The following screenshot shows an example **Events** page with a single ongoing event\. This active event is also flagged in the left navigation pane\. 

![\[The AWS Shield console left navigation pane has the Events selection highlighted in red, with a numeral 1 beside it, inside a red circle. The Events page is open, and shows a single row in the events list. The row lists an AWS resource of type CloudFront distribution. The Current status field contains a triangular red icon next to the words Mitigation in progress. The Attack vectors status field contains UDP traffic. The Start time field contains Sep 16th 2020, 2:43:00 pm SAST. The Duration field contains 6 minutes.\]](http://docs.aws.amazon.com/waf/latest/developerguide/)

Shield Advanced might also automatically place mitigations against attacks, depending on the traffic type and on your configured protections\. These mitigations can protect your resource from receiving excess traffic or traffic that matches a known DDoS attack signature\.

The following screenshot shows an example **Events** listing where all events have been mitigated by Shield Advanced or have subsided on their own\. 

![\[A AWS Shield console page titled Events lists events that have been detected recently and their current status.\]](http://docs.aws.amazon.com/waf/latest/developerguide/)

**Protect your resources before an event**  
Improve the accuracy of event detection by protecting resources with Shield Advanced while they are receiving the normal expected traffic, before they are subject to a DDoS attack\.

In order to accurately report events for a protected resource, Shield Advanced must first establish a baseline of expected traffic patterns for it\.
+ Shield Advanced reports infrastructure layer events for resources after they've been protected for at least 15 minutes\.
+ Shield Advanced reports web application layer events for resources after they've been protected for at least 24 hours\. The accuracy of detection for application layer events is best after Shield Advanced has observed expected traffic for 30 days\. 

**To access events information in the AWS Shield console**

1. Sign in to the AWS Management Console and open the AWS WAF & Shield console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the AWS Shield navigation pane, choose **Events**\. The console shows the **Events** page\. 

1. From the **Events** page, you can select any event in the list to see additional summary information and details for the event\. 