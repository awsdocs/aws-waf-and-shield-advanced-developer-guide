# Shield Advanced Metrics<a name="set-ddos-alarms"></a>

## AWS Shield Advanced Metrics<a name="shield-metrics"></a>

AWS Shield Advanced includes the following metrics\.


| Metric | Description | 
| --- | --- | 
| DDoSDetected | Indicates a DDoS event for a particular Amazon Resource Name \(ARN\)\. Reporting criteria: Non\-zero value indicates a DDoS event\. Zero when there is no DDoS event detected\.  | 
| DDoSAttackBitsPerSecond | The number of bytes observed during a DDoS event for a particular Amazon Resource Name \(ARN\)\. This metric is only available for layer 3/4 DDoS events\. Reporting criteria: Non\-zero value during an attack\. Zero when there is no attack\. Units: Bits  | 
| DDoSAttackPacketsPerSecond | The number of packets observed during a DDoS event for a particular Amazon Resource Name \(ARN\)\. This metric is only available for layer 3/4 DDoS events\. Reporting criteria: Non\-zero value during an attack\. Zero when there is no attack\. Units: Packets  | 
| DDoSAttackRequestsPerSecond | The number of requests observed during a DDoS event for a particular Amazon Resource Name \(ARN\)\. This metric is only available for layer 7 DDoS events and will only be reported for the most significant layer 7 events\. Reporting criteria: Non\-zero value during an attack\. Zero when there is no attack\. Units: Requests  | 

AWS Shield Advanced reports metrics to CloudWatch only when an attack on an AWS resource is detected\. If there are no attacks for a specified period, AWS Shield Advanced reports zero\.

Metrics for global resources, CloudFront and Route 53, are reported in the US East \(N\. Virginia\) Region\.

Shield Advanced posts the DDoSDetected metric with no other dimensions\. The other metrics include the appropriate AttackVector dimensions: 
+ UDPTraffic
+ UDPFragment
+ GenericUDPReflection
+ DNSReflection
+ NTPReflection
+ ChargenReflection
+ SSDPReflection
+ PortMapper
+ RIPReflection
+ SNMPReflection
+ MSSQLReflection
+ NetBIOSReflection
+ SYNFlood
+ ACKFlood
+ RequestFlood

### Creating AWS Shield Advanced Alarms<a name="shield-alarms"></a>

You can use these Shield Advanced metrics for CloudWatch alarms\. CloudWatch alarms send notifications or automatically make changes to the resources you are monitoring based on rules that you define\.

Detailed instructions for creating a CloudWatch alarm are in the [Amazon CloudWatch User Guide](http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/AlarmThatSendsEmail.html)\. When creating the alarm in the CloudWatch console, after choosing **Create an alarm**, choose **AWSDDOSProtectionMetrics** to use these Shield Advanced metrics\. You can then create an alarm based on a specific volume of traffic, or you can trigger the alarm whenever either of the above metrics is greater than zero\. Because Shield Advanced metrics are only reported when an attack is detected, the second option would trigger an alarm for any potential attack observed by Shield Advanced\.

**Note**  
The **AWSDDOSProtectionMetrics** are only available to Shield Advanced customers\.

For more information, see [What is CloudWatch](http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/WhatIsCloudWatch.html) in the *Amazon CloudWatch User Guide*\.