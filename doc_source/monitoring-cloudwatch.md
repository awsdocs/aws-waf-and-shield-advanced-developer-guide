# Monitoring with Amazon CloudWatch<a name="monitoring-cloudwatch"></a>

You can monitor web requests and web ACLs and rules using CloudWatch, which collects and processes raw data from AWS WAF into readable, near real\-time metrics\. These statistics are recorded for a period of two weeks, so that you can access historical information and gain a better perspective on how your web application or service is performing\.  For more information, see [What is CloudWatch](http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/WhatIsCloudWatch.html) in the *Amazon CloudWatch User Guide*\.

## Creating CloudWatch Alarms<a name="creating_alarms"></a>

You can create a CloudWatch alarm that sends an Amazon SNS message when the alarm changes state\. An alarm watches a single metric over a time period that you specify, and performs one or more actions based on the value of the metric relative to a specified threshold over a number of time periods\. The action is a notification sent to an Amazon SNS topic or Auto Scaling policy\. Alarms invoke actions for sustained state changes only\. CloudWatch alarms do not invoke actions simply because they are in a particular state; the state must have changed and been maintained for a specified number of periods\.

## AWS WAF and AWS Shield Advanced Metrics and Dimensions<a name="metrics_dimensions"></a>

 You can use the following procedures to view the metrics for AWS WAF and Shield Advanced\.

**Topics**

**To view metrics using the CloudWatch console**

Metrics are grouped first by the service namespace, and then by the various dimension combinations within each namespace\.

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. If necessary, change the region\. From the navigation bar, select the region where your AWS resources are located\. For more information, see [AWS Regions and Endpoints](http://docs.aws.amazon.com/general/latest/gr/rande.html)\.

   If you want to view AWS WAF metrics for CloudFront, you must choose the US East \(N\. Virginia\) region\.

1. In the navigation pane, choose **Metrics**\.

1. On the **All metrics** tab, choose the appropriate service\.

**To view metrics using the AWS CLI**
+ For AWS WAF, at a command prompt use the following command:

  ```
  1. aws cloudwatch list-metrics --namespace "WAF"
  ```

  For Shield Advanced, at a command prompt use the following command:

  ```
  1. aws cloudwatch list-metrics --namespace "DDoSProtection"
  ```

## AWS WAF Metrics<a name="waf-metrics"></a>

The `WAF` namespace includes the following metrics\.


| Metric | Description | 
| --- | --- | 
| `AllowedRequests` |  The number of allowed web requests\. Reporting criteria: There is a nonzero value Valid statistics: Sum  | 
| `BlockedRequests` |  The number of blocked web requests\. Reporting criteria: There is a nonzero value Valid statistics: Sum  | 
| `CountedRequests` |  The number of counted web requests\. Reporting criteria: There is a nonzero value A counted web request is one that matches all of the conditions in a particular rule\. Counted web requests are typically used for testing\. Valid statistics: Sum  | 
| `PassedRequests` |  The number of passed requests for a rule group\.  Reporting criteria: There is a nonzero value Passed requests are requests that did not match any rule contained in the rule group\. Valid statistics: Sum  | 

## AWS WAF Dimensions<a name="waf-metricdimensions"></a>

AWS WAF for CloudFront can use the following dimension combinations:
+ Rule, WebACL
+ RuleGroup, WebACL
+ Rule, RuleGroup

AWS WAF for Application Load Balancer can use the following dimension combinations:
+ Region, Rule, WebACL
+ Region, RuleGroup, WebACL
+ Region, Rule, RuleGroup


| Dimension | Description | 
| --- | --- | 
| `Rule` |  One of the following: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/waf/latest/developerguide/monitoring-cloudwatch.html)  | 
| `RuleGroup` |  The metric name of the RuleGroup\.  | 
| `WebACL` |  The metric name of the WebACL\.  | 
| `Region` |  The region of the application load balancer\.  | 

## Shield Advanced Metrics<a name="set-ddos-alarms"></a>

### AWS Shield Advanced Metrics<a name="shield-metrics"></a>

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
+ MemcachedReflection
+ SYNFlood
+ ACKFlood
+ RequestFlood

#### Creating AWS Shield Advanced Alarms<a name="shield-alarms"></a>

You can use these Shield Advanced metrics for CloudWatch alarms\. CloudWatch alarms send notifications or automatically make changes to the resources you are monitoring based on rules that you define\.

Detailed instructions for creating a CloudWatch alarm are in the [Amazon CloudWatch User Guide](http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/AlarmThatSendsEmail.html)\. When creating the alarm in the CloudWatch console, after choosing **Create an alarm**, choose **AWSDDOSProtectionMetrics** to use these Shield Advanced metrics\. You can then create an alarm based on a specific volume of traffic, or you can trigger the alarm whenever either of the above metrics is greater than zero\. Because Shield Advanced metrics are only reported when an attack is detected, the second option would trigger an alarm for any potential attack observed by Shield Advanced\.

**Note**  
The **AWSDDOSProtectionMetrics** are only available to Shield Advanced customers\.

For more information, see [What is CloudWatch](http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/WhatIsCloudWatch.html) in the *Amazon CloudWatch User Guide*\.