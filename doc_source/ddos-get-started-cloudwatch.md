# Step 5: Configure Amazon CloudWatch Alarms<a name="ddos-get-started-cloudwatch"></a>

You can monitor your protected resources for potential DDoS activity using CloudWatch alarms\. To create an alarm, you specify an Amazon SNS topic for your resources in each Region\. AWS Shield Advanced configures the SNS topic in CloudWatch to send you an email that alerts you to potential DDoS activity\.

**Note**  
CloudWatch incurs additional costs\. For CloudWatch pricing, see [Amazon CloudWatch Pricing](https://aws.amazon.com/cloudwatch/pricing/)\.

To create a CloudWatch alarm, follow the instructions in [Using Amazon CloudWatch Alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html)\.

By default, Shield Advanced configures CloudWatch to alert you after just one indicator of a potential DDoS event\. If needed, you can use the CloudWatch console to change this setting to alert you only after multiple indicators are detected\. 

You can continue from this step without configuring CloudWatch alarms\. However, doing so significantly reduces your visibility of possible DDoS events\.

**Note**  
In addition to the Amazon SNS notifications, you can also use a CloudWatch dashboard to monitor potential DDoS activity\. The dashboard collects and processes raw data from Shield Advanced into readable, near real\-time metrics\. These statistics are recorded for a period of two weeks, so that you can access historical information and gain a better perspective on how your web application or service is performing\. For more information, see [What is CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/WhatIsCloudWatch.html) in the *Amazon CloudWatch User Guide*\.  
For instructions on creating a CloudWatch dashboard, see [Monitoring with Amazon CloudWatch](monitoring-cloudwatch.md)\. For information about specific Shield Advanced metrics that you can add to your dashboard, see [AWS Shield Advanced Metrics and Alarms](monitoring-cloudwatch.md#set-ddos-alarms)\. 

After you configure the CloudWatch alarms, we recommend that you follow the instructions in [Step 6: Deploy AWS WAF Rules](deploy-waf-automations.md)\.