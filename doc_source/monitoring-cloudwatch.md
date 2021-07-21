# Monitoring with Amazon CloudWatch<a name="monitoring-cloudwatch"></a>

You can monitor web requests and web ACLs and rules using Amazon CloudWatch, which collects and processes raw data from AWS WAF and AWS Shield Advanced into readable, near real\-time metrics\. You can use statistics in Amazon CloudWatch to gain a perspective on how your web application or service is performing\.  For more information, see [What is CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/WhatIsCloudWatch.html) in the *Amazon CloudWatch User Guide*\.

**Note**  
CloudWatch metrics and alarms are not enabled for Firewall Manager\.

## Creating Amazon CloudWatch alarms<a name="creating_alarms"></a>

You can create an Amazon CloudWatch alarm that sends an Amazon SNS message when the alarm changes state\. An alarm watches a single metric over a time period that you specify, and performs one or more actions based on the value of the metric relative to a specified threshold over a number of time periods\. The action is a notification sent to an Amazon SNS topic or Auto Scaling policy\. Alarms invoke actions for sustained state changes only\. CloudWatch alarms do not invoke actions simply because they are in a particular state; the state must have changed and been maintained for a specified number of periods\.

## AWS WAF and AWS Shield Advanced metrics and dimensions<a name="metrics_dimensions"></a>

 You can use the following procedures to view the metrics for AWS WAF and AWS Shield Advanced\.

**Note**  
Amazon CloudWatch metrics and alarms are not enabled for AWS Firewall Manager\.

**To view metrics using the CloudWatch console**

Metrics are grouped first by the service namespace, and then by the various dimension combinations within each namespace\.

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. If necessary, change the Region\. From the navigation bar, choose the Region where your AWS resources are located\. For more information, see [AWS service endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html)\. 

   To view AWS WAF metrics for CloudFront, you must choose the US East \(N\. Virginia\) Region\.

1. In the navigation pane, choose **Metrics**\.

1. On the **All metrics** tab, choose the appropriate service\.

**To view metrics using the AWS CLI**
+ For AWS/WAFV2, at a command prompt use the following command:

  ```
  1. aws cloudwatch list-metrics --namespace "AWS/WAFV2"
  ```

  For Shield Advanced, at a command prompt use the following command:

  ```
  1. aws cloudwatch list-metrics --namespace "AWS/DDoSProtection"
  ```

## AWS WAF metrics and dimensions<a name="waf-metrics"></a>

The `WAF` namespace includes the following metrics and dimensions\.


**Web ACL, rule group, and rule metrics**  

| Metric | Description | 
| --- | --- | 
| `AllowedRequests` |  The number of allowed web requests\. Reporting criteria: There is a nonzero value\. Valid statistics: Sum  | 
| `BlockedRequests` |  The number of blocked web requests\. Reporting criteria: There is a nonzero value\. Valid statistics: Sum  | 
| `CountedRequests` |  The number of counted web requests\. Reporting criteria: There is a nonzero value\. A counted web request is one that matches at least one of the rules\. Request counting is typically used for testing\. Valid statistics: Sum  | 
| `PassedRequests` |  The number of passed requests\. This is only used for requests that go through a rule group evaluation without matching any of the rule group rules\.  Reporting criteria: There is a nonzero value\. Passed requests are requests that don't match any of the rules in the rule group\.  Valid statistics: Sum  | 


**Web ACL, rule group, and rule dimensions**  

| Dimension | Description | 
| --- | --- | 
|  `Region`  | Required for all protected resource types except for Amazon CloudFront distributions\. | 
|  `Rule`  |  One of the following: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/waf/latest/developerguide/monitoring-cloudwatch.html)  | 
|  `RuleGroup`  |  The metric name of the `RuleGroup`\.  | 
|  `WebACL`  |  The metric name of the `WebACL`\.  | 


**Label and AWS WAF Bot Control metrics**  

| Metric | Description | 
| --- | --- | 
|  `AllowedRequests`  |  The number of labels applied to web requests by rules that had an allow action setting\.  Reporting criteria: There is a nonzero value\. Valid statistics: Sum  | 
|  `BlockedRequests`  |  The number of labels applied to web requests by rules that had a block action setting\.  Reporting criteria: There is a nonzero value\. Valid statistics: Sum  | 
|  `CountedRequests`  |  The number of labels applied to web requests by rules that had a count action setting\.  Reporting criteria: There is a nonzero value\. Valid statistics: Sum  | 


**Label and AWS WAF Bot Control dimensions**  

| Dimension | Description | 
| --- | --- | 
|  `Region`  | Required for all protected resource types except for Amazon CloudFront distributions\. | 
|  `WebACL`  |  The metric name of the `WebACL`\.  | 
|  `RuleGroup`  |  The metric name of the `RuleGroup`\. Used for the metric `CountedRequests`\.  | 
|  `LabelNamespace`  | The namespace prefix of the web ACL or rule group where the matching rule is specified\. Used for the metrics AllowedRequests and BlockedRequests\. | 
|  `Label`  | The label applied to the web request by the matching rule\. Used for the metrics AllowedRequests and BlockedRequests\. | 


**Free bot visibility metrics**  

| Metric | Description | 
| --- | --- | 
|  `SampleAllowedRequests`  |  The percentage of sampled requests that have allow action\.  Reporting criteria: There is a nonzero value\. Valid statistics: Sum  | 
|  `SampleBlockedRequests`  |  The percentage of sampled requests that have block action\.  Reporting criteria: There is a nonzero value\. Valid statistics: Sum  | 


**Free bot visibility dimensions**  

| Dimension | Description | 
| --- | --- | 
|  `Region`  | Required for all protected resource types except for Amazon CloudFront distributions\. | 
|  `WebACL`  |  The metric name of the `WebACL`\.  | 
|  `BotCategory`  |  The metric name of the of the detected bot category, based on the web request labels\.   | 

## AWS Shield Advanced metrics and alarms<a name="set-ddos-alarms"></a>

This section discusses the metrics and alarms available with AWS Shield Advanced\.

### AWS Shield Advanced metrics<a name="shield-metrics"></a>

Shield Advanced reports metrics to Amazon CloudWatch on an AWS resource more frequently during DDoS events than while no events are underway\. Shield Advanced reports metrics once a minute during an event, and then once right after the event ends\. While no events are underway, Shield Advanced reports metrics once a day, at a time assigned to the resource\. This periodic report keeps the metrics active and available for use in custom CloudWatch alarms\. 

For the global services Amazon CloudFront and Amazon Route 53 , metrics are reported in the US East \(N\. Virginia\) Region\.

#### Detection metrics<a name="ddos-metrics-detection"></a>

Shield Advanced provides the following detection metrics and dimensions\. 


**Detection metrics**  

| Metric | Description | 
| --- | --- | 
| DDoSDetected | Indicates whether a DDoS event is underway for a particular Amazon Resource Name \(ARN\)\. This metric has a value of 1 during an event and a value of 0 otherwise\.   | 
| DDoSAttackBitsPerSecond | The number of bits observed during a DDoS event for a particular Amazon Resource Name \(ARN\)\. This metric is available only for layer 3 and layer 4 DDoS events\. This metric has a non\-zero value during an event and a value of 0 otherwise\.Units: Bits  | 
| DDoSAttackPacketsPerSecond | The number of packets observed during a DDoS event for a particular Amazon Resource Name \(ARN\)\. This metric is available only for layer 3 and layer 4 DDoS events\. This metric has a non\-zero value during an event and a value of 0 otherwise\.Units: Packets  | 
| DDoSAttackRequestsPerSecond | The number of requests observed during a DDoS event for a particular Amazon Resource Name \(ARN\)\. This metric is available only for layer 7 DDoS events\. The metric is reported only for the most significant layer 7 events\. This metric has a non\-zero value during an event and a value of 0 otherwise\.Units: Requests  | 

Shield Advanced posts the `DDoSDetected` metric with no other dimensions\. The remaining detection metrics include the `AttackVector` dimensions that correspond to the type of attack, from the following list:
+ `ACKFlood`
+ `ChargenReflection`
+ `DNSReflection`
+ `GenericUDPReflection`
+ `MemcachedReflection`
+ `MSSQLReflection`
+ `NetBIOSReflection`
+ `NTPReflection`
+ `PortMapper`
+ `RequestFlood`
+ `RIPReflection`
+ `SNMPReflection`
+ `SSDPReflection`
+ `SYNFlood`
+ `UDPFragment`
+ `UDPTraffic`
+ `UDPReflection`

#### Mitigation metrics<a name="ddos-metrics-mitigation"></a>

Shield Advanced provides the following mitigation metrics and dimensions\. 


**Mitigation metrics**  

| Metric | Description | 
| --- | --- | 
| VolumePacketsPerSecond | The number of packets per second that were dropped or passed by a mitigation that was deployed in response to a detected event\.Units: packets  | 


**Mitigation dimensions**  

| Dimension | Description | 
| --- | --- | 
|  `ResourceArn`  |  Amazon Resource Name \(ARN\)  | 
|  `MitigationAction`  |  The outcome of an applied mitigation\. Possible values are `Pass` or `Drop`\.   | 

#### Top contributors metrics<a name="ddos-metrics-top-contributors"></a>

Shield Advanced provides the following top contributors metrics and dimensions\. 


**Top contributors metrics**  

| Metric | Description | 
| --- | --- | 
| VolumePacketsPerSecond | The number of packets per second for a top contributor\.Units: packets  | 
| VolumeBitsPerSecond | The number of bits per second for a top contributor\. Units: bits  | 

Shield Advanced posts top contributors metrics by dimension combinations that characterize the event contributors\. You can use any of the following combinations of dimensions for any of the top contributors metrics:
+ `ResourceArn`, `Protocol` 
+ `ResourceArn`, `Protocol`, `SourcePort` 
+ `ResourceArn`, `Protocol`, `DestinationPort` 
+ `ResourceArn`, `Protocol`, `SourceIp` 
+ `ResourceArn`, `Protocol`, `SourceAsn` 
+ `ResourceArn`, `TcpFlags` 


**Top contributors dimensions**  

| Dimension | Description | 
| --- | --- | 
|  `ResourceArn`  |   Amazon Resource Name \(ARN\)\.  | 
|  `Protocol`  |  IP protocol name, either `TCP` or `UDP`\.  | 
|  `SourcePort`  |  Source TCP or UDP port\.  | 
|  `DestinationPort`  |  Destination TCP or UDP port\.  | 
|  `SourceIp`  |  Source IP address\.  | 
|  `SourceAsn`  |  Source autonomous system number \(ASN\)\.  | 
|  `TcpFlags `  |  A combination of flags present in a TCP packet, separated by a dash \(`-`\)\. Monitored flags are `ACK`, `FIN`, `RST`, `SYN`\. This dimension value always appears sorted alphabetically\. For example, `ACK-FIN-RST-SYN`, `ACK-SYN`, and `FIN-RST`\.  | 

### Creating AWS Shield Advanced alarms<a name="shield-alarms"></a>

You can use AWS Shield Advanced metrics for Amazon CloudWatch alarms\. CloudWatch sends notifications or automatically make changes to the resources that you are monitoring based on rules that you define\.

For detailed instructions on creating a CloudWatch alarm, see the [Amazon CloudWatch User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/AlarmThatSendsEmail.html)\. When creating the alarm on the CloudWatch console, to use the Shield Advanced metrics, after choosing **Create an alarm**, choose **AWSDDOSProtectionMetrics** \. You can then create an alarm based on a specific volume of traffic, or you can trigger an alarm whenever a metric is non\-zero\. The second option triggers an alarm for any potential attack that Shield Advanced observes\.

**Note**  
The **AWSDDOSProtectionMetrics** are available only to Shield Advanced customers\.

For more information, see [What is CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/WhatIsCloudWatch.html) in the *Amazon CloudWatch User Guide*\.

## AWS Firewall Manager notifications<a name="set-fms-alarms"></a>

AWS Firewall Manager doesn't record metrics, so you can't create Amazon CloudWatch alarms specifically for Firewall Manager\. However, you can configure Amazon SNS notifications to alert you to potential attacks\. To create Amazon SNS notifications in Firewall Manager, see [To create an Amazon SNS topic in Firewall Manager \(console\)](get-started-fms-shield-cloudwatch.md#get-started-fms-shield-sns-procedure)\.