# Amazon Kinesis Data Firehose<a name="logging-kinesis"></a>

To send logs to Amazon Kinesis Data Firehose, you send logs from your web ACL to an Amazon Kinesis Data Firehose with a configured storage destination\. After you enable logging, AWS WAF delivers logs to your storage destination through the HTTPS endpoint of Kinesis Data Firehose\. 

For information about how to create an Amazon Kinesis Data Firehose and review your stored logs, see [What Is Amazon Kinesis Data Firehose?](https://docs.aws.amazon.com/firehose/latest/dev/what-is-this-service.html) To understand the permissions required for your Kinesis Data Firehose configuration, see [Controlling Access with Amazon Kinesis Data Firehose](https://docs.aws.amazon.com/firehose/latest/dev/controlling-access.html)\.

You must have the following permissions to successfully enable logging with an Amazon Kinesis Data Firehose:
+ `iam:CreateServiceLinkedRole`
+ `firehose:ListDeliveryStreams`
+ `wafv2:PutLoggingConfiguration`

For information about service\-linked roles and the `iam:CreateServiceLinkedRole` permission, see [Using service\-linked roles for AWS WAF](using-service-linked-roles.md)\.

For more information about creating your delivery stream, see [Creating an Amazon Kinesis Data Firehose Delivery Stream](https://docs.aws.amazon.com/firehose/latest/dev/basic-create.html)\.

Configure an Amazon Kinesis Data Firehose delivery stream for your web ACL as follows\.
+ Create it using the same account as you use to manage the web ACL\.
+ Create it in the same Region as the web ACL\. If you are capturing logs for Amazon CloudFront, create the firehose in US East \(N\. Virginia\) Region, `us-east-1`\.
+ Give the data firehose a name that starts with the prefix `aws-waf-logs-`\. For example, `aws-waf-logs-us-east-2-analytics`\.
+ Configure it for direct put, which allows applications to access the delivery stream directly\. In the Amazon Kinesis Data Firehose console, for the delivery stream **Source** setting, choose **Direct PUT or other sources**\. Through the API, set the delivery stream property `DeliveryStreamType` to `DirectPut`\.
**Note**  
Do not use a `Kinesis stream` as your source\.

One AWS WAF log is equivalent to one Kinesis Data Firehose record\. If you typically receive 10,000 requests per second and you enable full logs, you should have a 10,000 records per second setting in Kinesis Data Firehose\. If you don't configure Kinesis Data Firehose correctly, AWS WAF won't record all logs\. For more information, see [Amazon Kinesis Data Firehose Quotas](https://docs.aws.amazon.com/firehose/latest/dev/limits.html)\. 