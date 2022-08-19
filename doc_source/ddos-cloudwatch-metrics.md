# AWS Shield Advanced Amazon CloudWatch metrics<a name="ddos-cloudwatch-metrics"></a>

Shield Advanced publishes Amazon CloudWatch event metrics for all resources that it protects\. These metrics improve your ability to monitor your resources by making it possible to create and configure CloudWatch dashboards and alarms for them\. 


**Shield Advanced Amazon CloudWatch metrics**  

| Metric | Description | 
| --- | --- | 
|  `DDoSDetected`  |  Indicates a DDoS event for a specific Amazon Resource Name \(ARN\)\. This metric has a value of 1 during an event and a value of 0 otherwise\.  | 
|  `DDoSAttackBitsPerSecond`  |  The number of bytes observed during a DDoS event for a specific ARN\. This metric is available only for network and transport layer \(layer 3 or 4\) DDoS events\. The unit of this metric is bits\.  | 
|  `DDoSAttackPacketsPerSecond`  |  The number of packets observed during a DDoS event for a specific ARN\. This metric is available only for network and transport layer \(layer 3 or 4\) DDoS events\. The unit of this metric is packets\.  | 
|  `DDoSAttackRequestsPerSecond`  |  The number of requests observed during a DDoS event for a specific ARN\. This metric is available only for application layer \(layer 7\) DDoS events\. The unit of this metric is requests\.  | 

If there are no events to record to a CloudWatch metric, once each day, Shield Advanced publishes a zero value metric\. This keeps the metric active and available for use in custom CloudWatch alarms and dashboards\. 

We recommend that you create alarms to notify you of circumstances that require attention\. As a starting point, you could create an alarm for each protected resource that reports when the `DDoSDetected` metric is non zero\. A non\-zero value in this metric doesn't necessarily imply that a DDoS attack is underway, but we recommend looking closer at the resource status when the metric is in this state\. 

For request floods, we recommend that you create alarms for composite checks that also consider factors such as application health and web request volume\. You may choose to alarm on the other three metrics that report on the volume of traffic for various attack vector dimensions\. By considering the capacity of your application and alarming when traffic is approaching your application limitations, you can create a set of rules that notify you as needed, without too much unwanted noise\. 

For additional information about Shield Advanced metrics, including mitigation and top contributor metrics, metric dimensions, and information about creating alarms, see [AWS Shield Advanced metrics and alarms](monitoring-cloudwatch.md#set-ddos-alarms)\.