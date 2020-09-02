# Logging and monitoring in AWS WAF<a name="waf-incident-response"></a>

Monitoring is an important part of maintaining the reliability, availability, and performance of AWS WAF and your AWS solutions\. You should collect monitoring data from all parts of your AWS solution so that you can more easily debug a multi\-point failure if one occurs\. AWS provides several tools for monitoring your AWS WAF resources and responding to potential events:

**Amazon CloudWatch Alarms**  
Using CloudWatch alarms, you watch a single metric over a time period that you specify\. If the metric exceeds a given threshold, CloudWatch sends a notification to an Amazon SNS topic or AWS Auto Scaling policy\. For more information, see [Monitoring with Amazon CloudWatch](monitoring-cloudwatch.md)\.

**AWS CloudTrail Logs**  
CloudTrail provides a record of actions taken by a user, role, or an AWS service in AWS WAF\. Using the information collected by CloudTrail, you can determine the request that was made to AWS WAF, the IP address from which the request was made, who made the request, when it was made, and additional details\. For more information, see [Logging API calls with AWS CloudTrail](logging-using-cloudtrail.md)\. 