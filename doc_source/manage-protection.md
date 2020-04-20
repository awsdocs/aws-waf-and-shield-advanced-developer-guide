# Managing AWS Shield Advanced protections<a name="manage-protection"></a>

You can change the settings for your AWS Shield Advanced protections at any time\. To do this, you walk through the options for all of your protections, making changes to the settings that you need to change\.

**To manage protections**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Protected resources**\.

1. Choose **Manage existing protections**\.

1. Walk through each of the options, making changes as needed and saving them as you go, or skipping the pages that you don't want to change\. The topics that follow cover each of the options\. 

## Add web ACLs and rules<a name="add-rule-ddos"></a>

For protection against attacks on Amazon CloudFront and Application Load Balancer resources, you can add AWS WAF web ACLs and rate\-based rules\. For information about how AWS WAF works, see [AWS WAF](waf-chapter.md)\. 

If you use Shield Advanced within an AWS Firewall Manager Shield Advanced policy, you can't add a web ACL or rate\-based rule\.

**To add web ACLs and rules**

1. In the protections page **Add web ACLs and rules**, you can choose an existing web ACL or create your own\. 
**Note**  
If a resource is already associated with a web ACL, you can't change to a different web ACL\. You must first remove the associated web ACLs from the resource\. For more information about removing a web ACL association, see [Associating or disassociating a Web ACL with an AWS resource](web-acl-associating-aws-resource.md)\.

   To create your own web ACL, follow these steps:

   1. Choose **Create new web ACL** from the dropdown list\.

   1. Enter a name\. You can't change the name after you create the web ACL\.

   1. Choose **Create web ACL**\.

1. For each resource that is listed in the table that doesn't have a rate\-based rule defined, you can add one by selecting the action **Add one** and then performing the following steps:

   1. Enter a name\.

   1. Enter a rate limit\. This is the maximum number of requests allowed in a five\-minute period from any single IP address\. 

   1. Choose the action to take if the rule is triggered\. **Block** will block requests\. **Count** will allow requests but increment a counter tracking how many times this rule was triggered\.

   1. Choose **Create rule**\.

1. Choose **Apply web ACLS and rules**\. 

## Configure health based DDoS detection<a name="associate-health-check"></a>

You can use your Amazon Route 53 health checks to improve how AWS Shield Advanced detects and mitigates network\-layer, transport\-layer, and application layer attacks\. For information about how this works, see [Shield Advanced health\-based detection](ddos-overview.md#ddos-advanced-health-check-option)\.

To get started with health\-based detection, create a Route 53 health check for the AWS resource that you want to protect with Shield Advanced\. For information about Route 53 health checks, see [How Amazon Route 53 Checks the Health of Your Resources](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/welcome-health-checks.html) and [Creating and Updating Health Checks](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/health-checks-creating.html)\. After you create your health check, associate it with your protection using the following procedure\. 

**Note**  
You are responsible for ensuring that the health check you use is relevant to the health of the protected resource and that it remains available for use by the protection\. Shield Advanced doesn't manage the health check in any way\. 

The following procedure shows how to associate an Amazon Route 53 health check with a protection\. 

**To configure health based DDoS detection**

1. In the protections page **Configure health based DDoS detection**, for the resource that you want to manage, under **Associated Health Check**, choose the ID of the health check that you want to associate with the protection\. 
**Note**  
If you don't see the health check you need, go to the Route 53 console and verify the health check and its ID\. For information, see [Creating and Updating Health Checks](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/health-checks-creating.html)\.

1. Choose **Associate health checks**\. 

**Shield Advanced health check status settings**  
The status of the health check that you associate with a protection can have the following values in the Shield console: 
+ **Healthy** — The health check is available and is reporting healthy\.
+ **Unhealthy** — The health check is available and is reporting unhealthy\.
+ **Unavailable** — The health check is not available for use by Shield Advanced\. To resolve this, first disassociate the health check from the protection in Shield Advanced\. Then, in Route 53, create a new health check for the protection and note its ID\. Finally, associate the new health check with the protection following the procedure in this topic\. Don't try to reassociate a health check that has been unavailable\.

## Create Amazon CloudWatch alarms and notifications<a name="add-alarm-ddos"></a>

The following procedure shows how to manage CloudWatch alarms for protected resources\. 

**Note**  
CloudWatch incurs additional costs\. For CloudWatch pricing, see [Amazon CloudWatch Pricing](https://aws.amazon.com/cloudwatch/pricing/)\.<a name="add-cw-procedure"></a>

**To create Amazon CloudWatch alarms and notifications**

1. In the protections page **Create Amazon CloudWatch alarms and notifications**, configure the SNS topics for the alarms and notifications that you want to receive\. For resources that you don't want notifications for, choose **No topic**\. You can add an Amazon SNS topic or create a different topic\. 

1. To create an Amazon SNS topic, follow these steps:

   1. Choose **Create new topic** from the dropdown list\.

   1. Enter a topic name\. 

   1. Enter an email address that the Amazon SNS messages will be sent to, and then choose **Add email address**\.

   1. Choose **Create topic**\.

   1. Repeat as necessary for each protection and each rate\-based rule\.

1. Choose **Create alarms**\.