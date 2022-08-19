# How AWS Shield detects events<a name="ddos-event-detection"></a>

AWS operates service\-level detection systems for the AWS network and individual AWS services, to ensure that they remain available during a DDoS attack\. Additionally, resource\-level detection systems monitor each individual AWS resource to ensure that traffic toward the resource remains within expected parameters\. This combination protects both the targeted AWS resource and AWS services, by applying mitigations that drop known bad packets, highlight potentially malicious traffic, and prioritize traffic from end users\.

Detected events appear in your Shield Advanced event summaries, attack details, and Amazon CloudWatch metrics as either the name of the DDoS attack vector or as `Volumetric` if the evaluation was based on traffic volume instead of signature\. For more information on the attack vector dimensions that are available within the `DDoSDetected` CloudWatch metric, see [AWS Shield Advanced metrics and alarms](monitoring-cloudwatch.md#set-ddos-alarms)

**Topics**
+ [Detection logic for infrastructure layer threats](ddos-event-detection-infrastructure.md)
+ [Detection logic for application layer threats](ddos-event-detection-application.md)
+ [Detection logic for multiple resources in an application](ddos-event-detection-multiple-resources.md)