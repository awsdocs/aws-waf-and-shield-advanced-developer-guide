# Managing AWS Shield Advanced protections<a name="manage-protection"></a>

You can change the settings for your AWS Shield Advanced protections at any time\. To do this, walk through the options for all of your protections and modify the settings that you need to change\.

**Note**  
The console guidance provided here is for the latest version of the AWS Shield console, released in 2020\. In the console, you can switch between versions\. 

**To manage protections**

1. Sign in to the AWS Management Console and open the AWS WAF & Shield console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the AWS Shield navigation pane, choose **Protected resources**\.

1. If you want to manage specific resources, select them\. 

1. Choose **Configure protections** and the resource specification option that you want\.

1. Walk through each of the resource protection options, making changes as needed\. The topics that follow cover each of the options\. 

## Configure layer 7 DDoS mitigation<a name="add-rule-ddos"></a>

For protection against attacks on Amazon CloudFront and Application Load Balancer resources, you can add AWS WAF web ACLs and rate\-based rules\. For information about how AWS WAF works, see [AWS WAF](waf-chapter.md)\. 

If you use Shield Advanced within an AWS Firewall Manager Shield Advanced policy, you can't add a web ACL or rate\-based rule\.

**To add web ACLs and rules**

1. In the **Configure layer 7 DDoS mitigation** page, if the resource isn't already associated with a web ACL, you can choose an existing web ACL or create your own\. 

   To create a web ACL, follow these steps:

   1. Choose **Create web ACL**\.

   1. Enter a name\. You can't change the name after you create the web ACL\.

   1. Choose **Create**\.
**Note**  
If a resource is already associated with a web ACL, you can't change to a different web ACL\. If you want to change the web ACL, you must first remove the associated web ACLs from the resource\. For more information, see [Associating or disassociating a Web ACL with an AWS resource](web-acl-associating-aws-resource.md)\.

   To create your own web ACL, follow these steps:

1. For each associated web ACL that doesn't have a rate\-based rule defined, you can add one by choosing **Add rate limit rule** and then performing the following steps:

   1. Enter a name\.

   1. Enter a rate limit\. This is the maximum number of requests allowed in any five\-minute period from any single IP address before the rate\-based rule action is applied to the IP address\. When the requests from the IP address fall below the limit, the action is discontinued\. 

   1. Set the rule action to count or block requests from IP addresses while their request counts are over the limit\. The application and removal of the rule action might take effect a minute or two after the IP address request rate changes\. 

   1. Choose **Add rule**\.

1. Choose **Next**\. 

## Configure health check based DDoS detection<a name="associate-health-check"></a>

You can use your Amazon Route 53 health checks to improve how AWS Shield Advanced detects and mitigates network\-layer, transport\-layer, and application layer attacks\. For information about how this works, see [Shield Advanced health\-based detection](ddos-overview.md#ddos-advanced-health-check-option)\.

To get started with health\-based detection, create a Route 53 health check for the AWS resource that you want to protect with Shield Advanced\. For information about Route 53 health checks, see [How Amazon Route 53 Checks the Health of Your Resources](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/welcome-health-checks.html) and [Creating and Updating Health Checks](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/health-checks-creating.html)\. After you create your health check, associate it with your protection using the following procedure\. 

**Note**  
You are responsible for ensuring that the health check you use is relevant to the health of the protected resource and that it remains available for use by the protection\. Shield Advanced doesn't manage the health check in any way\. 

The following procedure shows how to associate an Amazon Route 53 health check with a protection\. 

**To configure health\-based DDoS detection**

1. In the protections page **Configure health check based DDoS detection \- *optional***, for the resource that you want to manage, under **Associated Health Check**, choose the ID of the health check that you want to associate with the protection\. 
**Note**  
If you don't see the health check you need, go to the Route 53 console and verify the health check and its ID\. For information, see [Creating and Updating Health Checks](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/health-checks-creating.html)\.

1. Choose **Next**\. 

**Shield Advanced health check status settings**  
The status of the health check that you associate with a protection can have the following values in the Shield console: 
+ **Healthy** — The health check is available and is reporting healthy\.
+ **Unhealthy** — The health check is available and is reporting unhealthy\.
+ **Unavailable** — The health check is not available for use by Shield Advanced\. To resolve this, first disassociate the health check from the protection in Shield Advanced\. Then, in Route 53, create a new health check for the protection and note its ID\. Finally, associate the new health check with the protection following the procedure in this topic\. Don't try to reassociate a health check that has been unavailable\.

## Create alarms and notifications<a name="add-alarm-ddos"></a>

The following procedure shows how to manage CloudWatch alarms for protected resources\. 

**Note**  
CloudWatch incurs additional costs\. For CloudWatch pricing, see [Amazon CloudWatch Pricing](https://aws.amazon.com/cloudwatch/pricing/)\.<a name="add-cw-procedure"></a>

**To create alarms and notifications**

1. In the protections page **Create alarms and notifications \- *optional***, configure the SNS topics for the alarms and notifications that you want to receive\. For resources that you don't want notifications for, choose **No topic**\. You can add an Amazon SNS topic or create a new topic\. 

1. To create an Amazon SNS topic, follow these steps:

   1. In the dropdown list, choose **Create an SNS topic**\.

   1. Enter a topic name\. 

   1. Optionally enter an email address that the Amazon SNS messages will be sent to, and then choose **Add email**\. You can enter more than one\.

   1. Choose **Create**\.

1. Choose **Next**\.