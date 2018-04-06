# Step 4: Create a DDoS Dashboard in CloudWatch and set CloudWatch alarms<a name="deploy-waf-dashboard"></a>

You can monitor potential DDOS activity using CloudWatch, which collects and processes raw data from Shield Advanced into readable, near real\-time metrics\. These statistics are recorded for a period of two weeks, so that you can access historical information and gain a better perspective on how your web application or service is performing\. For more information, see [What is CloudWatch](http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/WhatIsCloudWatch.html) in the *Amazon CloudWatch User Guide*\.

Steps for creating a CloudWatch dashboard can be found in [Monitoring with Amazon CloudWatch](monitoring-cloudwatch.md)\. Specific Shield Advanced metrics you can add to your dashboard are listed in [Shield Advanced Metrics](set-ddos-alarms.md)\. 

After you create your dashboard, deploy AWS WAF rules using one or more of the resources described in [Step 5: Deploy AWS WAF Rules](deploy-waf-automations.md)\.