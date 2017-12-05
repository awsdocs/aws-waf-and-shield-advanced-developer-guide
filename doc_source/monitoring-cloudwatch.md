# Monitoring with Amazon CloudWatch<a name="monitoring-cloudwatch"></a>

You can monitor web requests and web ACLs and rules using CloudWatch, which collects and processes raw data from AWS WAF into readable, near real\-time metrics\. These statistics are recorded for a period of two weeks, so that you can access historical information and gain a better perspective on how your web application or service is performing\.  For more information, see [What is CloudWatch](http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/WhatIsCloudWatch.html) in the *Amazon CloudWatch User Guide*\.

## Creating CloudWatch Alarms<a name="creating_alarms"></a>

You can create a CloudWatch alarm that sends an Amazon SNS message when the alarm changes state\. An alarm watches a single metric over a time period that you specify, and performs one or more actions based on the value of the metric relative to a specified threshold over a number of time periods\. The action is a notification sent to an Amazon SNS topic or Auto Scaling policy\. Alarms invoke actions for sustained state changes only\. CloudWatch alarms do not invoke actions simply because they are in a particular state; the state must have changed and been maintained for a specified number of periods\.

## AWS WAF and AWS Shield Advanced Metrics and Dimensions<a name="metrics_dimensions"></a>

 You can use the following procedures to view the metrics for AWS WAF and Shield Advanced\.

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