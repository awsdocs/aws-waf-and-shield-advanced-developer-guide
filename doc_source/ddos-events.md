# AWS Shield Advanced events<a name="ddos-events"></a>

When you subscribe to Shield Advanced, and protect your resources, you gain access to additional visibility features for the resource applications that you have running on AWS\. These include near real\-time notification of events that are detected by Shield Advanced and additional information about detected events and mitigations\. 

Shield Advanced provides event summaries and details through the **Events** page of the Shield console\. You can get an overview of current and past events in the top level **Events** page\. 

**To access events information in the AWS Shield console**

1. Sign in to the AWS Management Console and open the AWS WAF & Shield console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the AWS Shield navigation pane, choose **Events**\.

The console **Events** page lists your events\. You can access summary and details for any event by selecting it from the list\.

**Protect your resources before an event**  
Improve the accuracy of event detection by protecting resources with Shield Advanced while they are receiving the normal expected traffic, before they are subject to a DDoS attack\.

In order to accurately report events for a protected resource, Shield Advanced must first establish a baseline of expected traffic patterns for it\.
+ Shield Advanced reports infrastructure layer events for resources after they've been protected for at least 15 minutes\.
+ Shield Advanced reports web application layer events for resources after they've been protected for at least 24 hours\. The accuracy of detection for application layer events is best after Shield Advanced has observed expected traffic for 30 days\. 