# Logging and monitoring in AWS WAF Classic<a name="classic-waf-incident-response"></a>

**Note**  
This is **AWS WAF Classic** documentation\. If you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November, 2019, and you have not migrated your web ACLs over yet, you need to use AWS WAF Classic to access those resources\. Otherwise, do not use this version\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

Monitoring is an important part of maintaining the reliability, availability, and performance of AWS WAF Classic and your AWS solutions\. You should collect monitoring data from all parts of your AWS solution so that you can more easily debug a multi\-point failure if one occurs\. AWS provides several tools for monitoring your AWS WAF Classic resources and responding to potential incidents:

**Amazon CloudWatch Alarms**  
Using CloudWatch alarms, you watch a single metric over a time period that you specify\. If the metric exceeds a given threshold, CloudWatch sends a notification to an Amazon SNS topic or AWS Auto Scaling policy\. For more information, see [Monitoring with Amazon CloudWatch](monitoring-cloudwatch.md)\.

**AWS CloudTrail Logs**  
CloudTrail provides a record of actions taken by a user, role, or an AWS service in AWS WAF Classic\. Using the information collected by CloudTrail, you can determine the request that was made to AWS WAF Classic, the IP address from which the request was made, who made the request, when it was made, and additional details\. For more information, see [Logging API calls with AWS CloudTrail](logging-using-cloudtrail.md)\.

**AWS Trusted Advisor**  
Trusted Advisor draws upon best practices learned from serving hundreds of thousands of AWS customers\. Trusted Advisor inspects your AWS environment and then makes recommendations when opportunities exist to save money, improve system availability and performance, or help close security gaps\. All AWS customers have access to five Trusted Advisor checks\. Customers with a Business or Enterprise support plan can view all Trusted Advisor checks\. For more information, see [AWS Trusted Advisor](https://docs.aws.amazon.com/awssupport/latest/user/getting-started.html#trusted-advisor)\.