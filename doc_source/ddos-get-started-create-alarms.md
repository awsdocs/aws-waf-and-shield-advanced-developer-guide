# Configure alarms and notifications<a name="ddos-get-started-create-alarms"></a>

You can optionally configure Amazon Simple Notification Service notifications for detected Amazon CloudWatch alarms and rate\-based rule activity\. You can use these to receive notification when Shield detects an event on a protected resource or when a rate\-limit configured in a rate\-based rule is exceeded\. 

For information about Shield Advanced CloudWatch metrics, see [AWS Shield Advanced Amazon CloudWatch metrics](ddos-cloudwatch-metrics.md)\. For information about Amazon SNS, see the [Amazon Simple Notification Service Developer Guide](https://docs.aws.amazon.com/sns/latest/dg/)\. 

**To configure alarms and notifications**

1. Select the Amazon SNS topics that you want notification for\. You can use a single Amazon SNS topic for all protected resources and rate\-based rules, or you can choose different topics, customized to your organization\. For example, you can create an SNS topic for each team that's responsible for incident response for a specific set of resources\.

1. Choose **Next**\. The console wizard advances to the resource protection review page\.