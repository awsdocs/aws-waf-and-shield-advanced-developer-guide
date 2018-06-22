# Step 4: Create a DDoS Dashboard in CloudWatch and Set CloudWatch Alarms<a name="deploy-waf-dashboard"></a>

You can monitor potential DDoS activity using CloudWatch, which collects and processes raw data from Shield Advanced into readable, near real\-time metrics\. These statistics are recorded for a period of two weeks, so that you can access historical information and gain a better perspective on how your web application or service is performing\. For more information, see [What is CloudWatch](http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/WhatIsCloudWatch.html) in the *Amazon CloudWatch User Guide*\.

For instructions for creating a CloudWatch dashboard, see [Monitoring with Amazon CloudWatch](monitoring-cloudwatch.md)\. For information about specific Shield Advanced metrics that you can add to your dashboard, see [Shield Advanced Metrics](monitoring-cloudwatch.md#set-ddos-alarms)\. 

After you create your CloudWatch dashboard, deploy AWS WAF rules using one or more of the resources that are described in [Step 5: Deploy AWS WAF Rules](deploy-waf-automations.md)\.