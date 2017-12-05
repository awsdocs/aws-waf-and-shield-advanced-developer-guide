# Shield Advanced Metrics<a name="set-ddos-alarms"></a>

## AWS Shield Advanced Metrics<a name="shield-metrics"></a>

AWS Shield Advanced includes the following metrics\.


| Metric | Description | 
| --- | --- | 
| RequestCount | The number of requests during an attack\. Reporting criteria: Non\-zero value during an attack\. Zero when there is no attack\. Statistics: The most useful statistic is Sum\. Units: Count  | 
| ByteCount | The number of bytes per second during an attack\. Reporting criteria: Non\-zero value during an attack\. Zero when there is no attack\. Statistics: The most useful statistic is Sum\. Units: Bytes  | 

AWS Shield Advanced reports metrics to CloudWatch only when an attack on an AWS resource is detected\. If there are no attacks for a specified period, AWS Shield Advanced reports zero\.

### Creating AWS Shield Advanced Alarms<a name="shield-alarms"></a>

You can use these Shield Advanced metrics for CloudWatch alarms\. CloudWatch alarms send notifications or automatically make changes to the resources you are monitoring based on rules that you define\.

Detailed instructions for creating a CloudWatch alarm are in the [Amazon CloudWatch User Guide](http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/AlarmThatSendsEmail.html)\. When creating the alarm in the CloudWatch console, after choosing **Create an alarm**, choose **AWSDDOSProtection Metrics** to use these Shield Advanced metrics\. You can then create an alarm based on a specific volume of traffic, or you can trigger the alarm whenever either of the above metrics is greater than zero\. Because Shield Advanced metrics are only reported when an attack is detected, the second option would trigger an alarm for any potential attack observed by Shield Advanced\.

**Note**  
The **AWSDDOSProtection Metrics** are only available to Shield Advanced customers\.

For more information, see [What is CloudWatch](http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/WhatIsCloudWatch.html) in the *Amazon CloudWatch User Guide*\.