# Managing AWS Shield Advanced protections<a name="manage-protection"></a>

You can change the settings for your AWS Shield Advanced protections at any time\. 

## Adding a Web ACL and rate\-based rule to your Shield Advanced protections<a name="add-rule-ddos"></a>

For protection against attacks on Amazon CloudFront and Application Load Balancer resources, you can add AWS WAF web ACLs and rate\-based rules\. For information about how AWS WAF works, see [AWS WAF](waf-chapter.md)\. 

The following procedure shows how to add a web ACL and rate\-based rule to a protection\.<a name="add-rule-procedure"></a>

**To add a web ACL and rate\-based rule to a protection**

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

   1. Enter a rate limit\. This is the maximum number of requests from a single IP address that are allowed in a five\-minute period\. 

   1. Choose **Create rule**\.

1. Choose the action to take if the rule is triggered\. **Block** will block the request\. **Count** will allow the request but increment a counter tracking how many times this rule was triggered\.

1. Choose **Apply web protections**\. 

1. To skip the Amazon CloudWatch alarms page, uncheck all the check boxes and choose **Create alarms**\. 

## Adding health\-based detection to your Shield Advanced protections<a name="associate-health-check"></a>

You can use your Amazon Route 53 health checks to improve how AWS Shield Advanced detects and mitigates network\-layer, transport\-layer, and application layer attacks\. For information about how this works, see [Shield Advanced health\-based detection](ddos-overview.md#ddos-advanced-health-check-option)\.

To get started with health\-based detection, create a Route 53 health check for the AWS resource that you want to protect with Shield Advanced\. For information about Route 53 health checks, see [How Amazon Route 53 Checks the Health of Your Resources](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/welcome-health-checks.html) and [Creating and Updating Health Checks](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/health-checks-creating.html)\. After you create your health check, associate it with your protection using the following procedure\. 

**Note**  
You are responsible for ensuring that the health check you use is relevant to the health of the protected resource and that it remains available for use by the protection\. Shield Advanced doesn't manage the health check in any way\. 

The following procedure shows how to associate an Amazon Route 53 health check with a protection\. 

**To associate a health check with a Shield Advanced protection**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. Choose **Protected resources**\.

1. Choose the resource that you want to edit\.

1. Choose **Manage existing protections**\.

1. If you need to skip the **Add web ACLs and rules** page, choose **Skip and go to next step**\. 

1. For **Configure enhanced DDoS detection**, choose the resource that you want to edit\. 

1. Under **Associated Health Check**, choose the ID of the health check that you want to associate with the protection\. 
**Note**  
If you don't see the health check you need, go to the Route 53 console and verify the health check and its ID\. For information, see [Creating and Updating Health Checks](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/health-checks-creating.html)\.

1. Choose **Associate Health Check**\. 

1. To skip the Amazon CloudWatch alarms page, either clear all the check boxes and choose **Finish** or choose **Cancel**\. Canceling only skips the CloudWatch settings and doesn't cancel your changes to the health check settings\. 

**Shield Advanced health check status settings**  
The status of the health check that you associate with a protection can have the following values in the Shield console: 
+ **Healthy** — The health check is available and is reporting healthy\.
+ **Unhealthy** — The health check is available and is reporting unhealthy\.
+ **Unavailable** — The health check is not available for use by Shield Advanced\. To resolve this, first disassociate the health check from the protection in Shield Advanced\. Then, in Route 53, create a new health check for the protection and note its ID\. Finally, associate the new health check with the protection following the procedure in this topic\. Don't try to reassociate a health check that has been unavailable\.

## Adding a CloudWatch alarm to your Shield Advanced protections<a name="add-alarm-ddos"></a>

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

## Removing a CloudWatch alarm from your Shield Advanced protections<a name="remove-cloudwatch-ddos"></a>

To remove a CloudWatch alarm from your Shield Advanced protections, you have two options:
+ Delete the protection as described in [Removing AWS Shield Advanced from an AWS resource](remove-protection.md)\. Be sure to select the check box next to **Also delete related DDoSDetection alarm**\.
+ Delete the alarm using the CloudWatch console\. The name of the alarm to delete will start with **DDoSDetectedAlarmForProtection**\.