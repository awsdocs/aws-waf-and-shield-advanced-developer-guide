# Monitoring AWS WAF, AWS Firewall Manager, and AWS Shield Advanced<a name="monitoring_overview"></a>

Monitoring is an important part of maintaining the reliability, availability, and performance of AWS WAF, AWS Firewall Manager, and AWS Shield Advanced and for identifying possible DDoS attacks using Shield Advanced\. As you start monitoring these services, you should create a monitoring plan that includes answers to the following questions:
+ What are your monitoring goals?
+ What resources will you monitor?
+ How often will you monitor these resources?
+ What monitoring tools will you use?
+ Who will perform the monitoring tasks?
+ Who should be notified when something goes wrong?

The next step is to establish a baseline for normal performance in your environment, by measuring performance at various times and under different load conditions\. As you monitor AWS WAF, Firewall Manager, Shield Advanced and related services, store historical monitoring data so that you can compare it with current performance data, identify normal performance patterns and performance anomalies, and devise methods to address issues\.

For AWS WAF, you should monitor the following items at a minimum to establish a baseline:
+ The number of allowed web requests
+ The number of blocked web requests

**Topics**
+ [Monitoring tools](monitoring_automated_manual.md)
+ [Logging API calls with AWS CloudTrail](logging-using-cloudtrail.md)