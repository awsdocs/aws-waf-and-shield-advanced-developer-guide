# Logging web ACL traffic<a name="logging"></a>

You can enable logging to get detailed information about traffic that is analyzed by your web ACL\. Logged information includes the time that AWS WAF received a web request from your AWS resource, detailed information about the request, and details about the rules that the request matched\. You can send your logs to an Amazon CloudWatch Logs log group, an Amazon Simple Storage Service \(Amazon S3\) bucket, or an Amazon Kinesis Data Firehose\.

## Pricing for logging web ACL traffic information<a name="logging-pricing"></a>

You are charged for logging web ACL traffic information according to the costs associated with each log destination type\. These charges are in addition to the charges for using AWS WAF\. Your costs can vary depending on factors such as the destination type that you choose and the amount of data that you log\. 

The following provides links to the pricing information for each logging destination type:
+ **CloudWatch Logs** – The charges are for vended log delivery\. See [Amazon CloudWatch Logs Pricing](http://aws.amazon.com/cloudwatch/pricing/)\. Under **Paid Tier**, choose the **Logs** tab, and then under **Vended Logs**, see the information for **Delivery to CloudWatch Logs**\.
+ **Amazon S3 buckets** – The Amazon S3 charges are the combined charges for CloudWatch Logs vended log delivery to the Amazon S3 buckets and for using Amazon S3\. 
  + For Amazon S3, see [Amazon S3 Pricing](http://aws.amazon.com/s3/pricing/)\. 
  + For CloudWatch Logs vended log delivery to the Amazon S3, see [Amazon CloudWatch Logs Pricing](http://aws.amazon.com/cloudwatch/pricing/)\. Under **Paid Tier**, choose the **Logs** tab, and then under **Vended Logs**, see the information for **Delivery to S3**
+ **Kinesis Data Firehose** – See [Amazon Kinesis Data Firehose Pricing](http://aws.amazon.com/kinesis/data-firehose/pricing/)\.

For information about AWS WAF pricing, see [AWS WAF Pricing](http://aws.amazon.com/waf/pricing/)\. 