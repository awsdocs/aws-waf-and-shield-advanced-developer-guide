# Monitoring Tools<a name="monitoring_automated_manual"></a>

AWS provides various tools that you can use to monitor AWS WAF and AWS Shield\. You can configure some of these tools to do the monitoring for you, while some of the tools require manual intervention\. We recommend that you automate monitoring tasks as much as possible\.

## Automated Monitoring Tools<a name="monitoring_automated_tools"></a>

You can use the following automated monitoring tools to watch AWS WAF and AWS Shield Advanced and report when something is wrong:
+ Not only can you use CloudWatch to monitor AWS WAF and Shield Advanced metrics as described in [Monitoring with Amazon CloudWatch](monitoring-cloudwatch.md), you also should use CloudWatch to monitor activity for your Amazon API Gateway and Elastic Load Balancing resources and Amazon CloudFront distributions\. For more information, see [Tracing, Logging, and Monitoring an API Gateway API](https://docs.aws.amazon.com/apigateway/latest/developerguide/monitoring_overview.html), [CloudWatch Metrics for Your Application Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-cloudwatch-metrics.html) and [Monitoring CloudFront Activity Using CloudWatch](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/monitoring-using-cloudwatch.html)\. 
+ **AWS CloudTrail Log Monitoring** – Share log files between accounts, monitor CloudTrail log files in real time by sending them to CloudWatch Logs, write log\-processing applications in Java, and validate that your log files have not changed after delivery by CloudTrail\. For more information, see [Logging API Calls with AWS CloudTrail](logging-using-cloudtrail.md) and [Working with CloudTrail Log Files](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-working-with-log-files.html) in the *AWS CloudTrail User Guide*\. 
+ **AWS Config** – View the configuration of AWS resources in your AWS account, including how the resources are related to one another and how they were configured in the past so that you can see how the configurations and relationships change over time\.

## Manual Monitoring Tools<a name="monitoring_manual_tools"></a>

Another important part of monitoring AWS WAF and AWS Shield involves manually monitoring those items that the CloudWatch alarms don't cover\. You can view the AWS WAF, AWS Shield Advanced, CloudWatch, and other AWS console dashboards to see the state of your AWS environment\. We recommend that you also check the log files for your web ACLs and rules\.
+ View the AWS WAF dashboard: 
  + On the **Requests** tab of the AWS WAF **Web ACLs** page, view a graph of total requests and requests that match each rule that you have created\. For more information, see [Viewing a Sample of the Web Requests That API Gateway CloudFront or an Application Load Balancer Has Forwarded to AWS WAF](web-acl-testing.md#web-acl-testing-view-sample)\.
+ View the CloudWatch home page for the following:
  + Current alarms and status
  + Graphs of alarms and resources
  + Service health status

  In addition, you can use CloudWatch to do the following:
  + Create [customized dashboards](https://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/CloudWatch_Dashboards.html) to monitor the services that you care about
  + Graph metric data to troubleshoot issues and discover trends
  + Search and browse all of your AWS resource metrics
  + Create and edit alarms to be notified of problems