# Managing AWS Shield Advanced Protections<a name="manage-protection"></a>

You can change the settings for your AWS Shield Advanced protections at any time\. For example, you can add or remove rate\-based rules and Amazon CloudWatch alarms\. 

## Adding a Web ACL and Rate\-based Rule to Your Shield Advanced Protections<a name="add-rule-ddos"></a>

The following procedure shows how to add a web ACL and rate\-based rule to a protected resource\.<a name="add-rule-procedure"></a>

**To add a web ACL and rate\-based rule to a protected resource**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. Choose **Protected resources**\.

1. Choose the radio button next to the resource that you want to edit\.

1. Choose **Manage existing protections**\.

1. Choose the check box next to the resource that you want to edit\.

1. Choose an existing web ACL and an existing rate\-based rule\. Alternatively, you can create a different web ACL and rate\-based rule by following these steps:

   1. Choose **Create new web ACL** from the dropdown list\.

   1. Enter a name\. You can't change the name after you create the web ACL\.

   1. Choose **Create web ACL**\.

   1. From the dropdown list, choose **Create new rule**\.

   1. Enter a name\.

   1. Enter a rate limit\. This is the maximum number of requests from a single IP address allowed in a five\-minute period\. The rate limit must be equal to or greater than 100\. 

   1. Choose **Create rule**\.

1. Choose the action to take if the rule is triggered\. **Block** will block the request\. **Count** will allow the request but increment a counter tracking how many times this rule was triggered\.

1. Choose **Apply web protections**\. 

1. To skip the Amazon CloudWatch alarms page, uncheck all the check boxes and choose **Create alarms**\. 

## Adding a CloudWatch Alarm to Your Shield Advanced Protections<a name="add-alarm-ddos"></a>

The following procedure shows how to add a CloudWatch alarm to a protected resource\. 

**Note**  
CloudWatch incurs additional costs\. For CloudWatch pricing, see [Amazon CloudWatch Pricing](https://aws.amazon.com/cloudwatch/pricing/)\.<a name="add-cw-procedure"></a>

**To add a CloudWatch alarm to a protected resource**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. Choose **Protected resources**\.

1. Choose the radio button next to the resource\.

1. Choose **Manage existing protections**\.

1. To skip the rate\-based rule page, choose **Continue**\.

1. For each Region that is listed in the table, choose an existing Amazon SNS topic or create a different topic\. To create an Amazon SNS topic, follow these steps:

   1. Choose **Create new topic** from the dropdown list\.

   1. Enter a topic name\. 

   1. Enter an email address that the Amazon SNS messages will be sent to, and then choose **Add email address**\.

   1. Choose **Create topic**\.

   1. Repeat as necessary for each protection and each rate\-based rule\.

1. Choose **Create alarms**\.

## Removing a CloudWatch Alarm from Your Shield Advanced Protections<a name="remove-cloudwatch-ddos"></a>

To remove a CloudWatch alarm from your Shield Advanced protections, you have two options:
+ Delete the protection as described in [Removing AWS Shield Advanced from an AWS Resource](remove-protection.md)\. Be sure to select the check box next to **Also delete related DDoSDetection alarm**\.
+ Delete the alarm using the CloudWatch console\. The name of the alarm to delete will start with **DDoSDetectedAlarmForProtection**\.