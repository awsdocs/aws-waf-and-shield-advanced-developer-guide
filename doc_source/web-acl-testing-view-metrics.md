# Viewing metrics for your web ACL<a name="web-acl-testing-view-metrics"></a>

After you've associated a web ACL with one or more AWS resources, you can view the resulting metrics for the association in an Amazon CloudWatch graph\. 

For information about CloudWatch metrics, see the [Amazon CloudWatch documentation](https://docs.aws.amazon.com/AmazonCloudWatch/)\. For a list of the metrics that AWS WAF provides, see [AWS WAF metrics and dimensions](monitoring-cloudwatch.md#waf-metrics)\.

For each rule in a web ACL and for all the requests that an associated resource forwards to AWS WAF for a web ACL, CloudWatch lets you do the following:
+ View data for the preceding hour or preceding three hours\.
+ Change the interval between data points\.
+ Change the calculation that CloudWatch performs on the data, such as maximum, minimum, average, or sum\.

**Note**  
AWS WAF with CloudFront is a global service and metrics are available only when you choose the **US East \(N\. Virginia\)** Region in the AWS Management Console\. If you choose another region, no AWS WAF metrics will appear in the CloudWatch console\.

**To view data for the rules in a web ACL**

1. Sign in to the AWS Management Console and open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. If necessary, change the Region to the one where your AWS resources are located\. For CloudFront, choose the US East \(N\. Virginia\) Region\.

1. In the navigation pane, under **Metrics**, choose **All metrics** and then search under the **Browse** tab for `AWS::WAFv2`\. 

1. Select the check box for the web ACL that you want to view data for\.

1. Change the applicable settings:  
**Statistic**  
Choose the calculation that CloudWatch performs on the data\.  
**Time range**  
Choose whether you want to view data for the preceding hour or the preceding three hours\.  
**Period**  
Choose the interval between data points in the graph\.  
**Rules**  
Choose the rules for which you want to view data\.

   Note the following:
   + If you recently associated a web ACL with an AWS resource, you might need to wait a few minutes for data to appear in the graph and for the metric for the web ACL to appear in the list of available metrics\.
   + If you associate more than one resource with a web ACL, the CloudWatch data will include requests for all of them\.
   + You can hover the cursor over a data point to get more information\.
   + The graph doesn't refresh itself automatically\. To update the display, choose the refresh \(![\[Icon to refresh the CloudWatch graph\]](http://docs.aws.amazon.com/waf/latest/developerguide/images/cloudwatch-refresh-icon.png)\) icon\.

For more information about CloudWatch metrics, see [Monitoring AWS WAF, AWS Firewall Manager, and AWS Shield Advanced](monitoring_overview.md)\. 