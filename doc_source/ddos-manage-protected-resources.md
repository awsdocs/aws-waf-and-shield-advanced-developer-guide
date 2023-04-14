# Managing resource protections in AWS Shield Advanced<a name="ddos-manage-protected-resources"></a>

Use the guidance in this section to manage Shield Advanced protections for your resources\. 

**Note**  
Shield Advanced protects only resources that you have specified either in Shield Advanced or through an AWS Firewall Manager Shield Advanced policy\. It doesn't automatically protect your resources\.

If you're using an AWS Firewall Manager Shield Advanced policy, you don't need to manage protections for resources that are in scope of the policy\. Firewall Manager automatically manages protections for accounts and resources that are in scope of a policy, according to the policy configuration\. For more information, see [AWS Shield Advanced policies](shield-policies.md)\.

**Topics**
+ [Adding AWS Shield Advanced protection to AWS resources](#configure-new-protection)
+ [Configuring AWS Shield Advanced protections](#manage-protection)
+ [Removing AWS Shield Advanced protection from an AWS resource](#remove-protection)

## Adding AWS Shield Advanced protection to AWS resources<a name="configure-new-protection"></a>

Follow the guidance in this section to add Shield Advanced protection to one or more resources\.

**To add protection for an AWS resource**

1. Sign in to the AWS Management Console and open the AWS WAF & Shield console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, under AWS Shield choose **Protected resources**\. 

1. Choose **Add resources to protect**\.

1. In the **Choose resources to protect with Shield Advanced** page, in **Specify the Region and resource types**, provide the Region and resource type specifications for the resources that you want to protect\. You can protect resources in multiple Regions by selecting **All Regions** and you can narrow the selection to global resources by selecting **Global**\. You can deselect any resource types that you do not want to protect\. For information about protections for your resource types, see [AWS Shield Advanced protections by resource type](ddos-protections-by-resource-type.md)\.

1. Choose **Load resources**\. Shield Advanced populates the **Select Resources** section with the AWS resources that match your criteria\. 

1. In the **Select Resources** section, you can filter the list of resources by entering a string to search for in the resource listings\. 

   Select the resources that you want to protect\.

1. In the **Tags** section, if you want to add tags to the Shield Advanced protections that you are creating, specify those\. For information about tagging AWS resources, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\. 

1. Choose **Protect with Shield Advanced**\. This adds Shield Advanced protections to the resources\.

## Configuring AWS Shield Advanced protections<a name="manage-protection"></a>

You can change the settings for your AWS Shield Advanced protections at any time\. To do this, walk through the options for your selected protections and modify the settings that you need to change\. 

**To manage protected resources**

1. Sign in to the AWS Management Console and open the AWS WAF & Shield console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the AWS Shield navigation pane, choose **Protected resources**\.

1. In the **Protections** tab, select the resources that you want to protect\. 

1. Choose **Configure protections** and the resource specification option that you want\.

1. Walk through each of the resource protection options, making changes as needed\. 

### Configure application layer DDoS protections<a name="configure-app-layer-protection"></a>

For protection against attacks on Amazon CloudFront and Application Load Balancer resources, you can add AWS WAF web ACLs and add rate\-based rules\. For information about this, see [Shield Advanced application layer AWS WAF web ACLs and rate\-based rules](ddos-app-layer-web-ACL-and-rbr.md)\.

You can also enable the Shield Advanced automatic application layer DDoS mitigation\. For information about how AWS WAF works, see [AWS WAF](waf-chapter.md)\. For information about the automatic mitigation feature, see [Shield Advanced automatic application layer DDoS mitigation](ddos-automatic-app-layer-response.md)\.

**Important**  
If you manage your Shield Advanced protections through AWS Firewall Manager using a Shield Advanced policy, you can't manage the application layer protections here\. For all other resources, we recommend that, at a minimum, you attach a web ACL to each resource, even if web ACL doesn't contain any rules\.

**Note**  
When you enable automatic application layer DDoS mitigation for a resource, if needed, the operation automatically adds a service\-linked role to your account to give Shield Advanced the permissions it needs to manage your web ACL protections\. For information, see [Using service\-linked roles for Shield Advanced](shd-using-service-linked-roles.md)[Using service\-linked roles for Shield Advanced](shd-using-service-linked-roles.md)\.

**To configure application layer DDoS protections**

1. In the **Configure layer 7 DDoS protections** page, if the resource isn't already associated with a web ACL, you can choose an existing web ACL or create your own\. 

   To create a web ACL, follow these steps:

   1. Choose **Create web ACL**\.

   1. Enter a name\. You can't change the name after you create the web ACL\.

   1. Choose **Create**\.
**Note**  
If a resource is already associated with a web ACL, you can't change to a different web ACL\. If you want to change the web ACL, you must first remove the associated web ACLs from the resource\. For more information, see [Associating or disassociating a web ACL with an AWS resource](web-acl-associating-aws-resource.md)\.

1. If the web ACL doesn't have a rate\-based rule defined, you can add one by choosing **Add rate limit rule** and then performing the following steps:

   1. Enter a name\.

   1. Enter a rate limit\. This is the maximum number of requests allowed in any five minute period from any single IP address before the rate\-based rule action is applied to the IP address\. When the requests from the IP address fall below the limit, the action is discontinued\. 

   1. Set the rule action to count or block requests from IP addresses while their request counts are over the limit\. The application and removal of the rule action might take effect a minute or two after the IP address request rate changes\. 

   1. Choose **Add rule**\.

1. For **Automatic application layer DDoS mitigation**, choose whether you want Shield Advanced to automatically mitigate DDoS attacks on your behalf, as follows: 
   + To enable automatic mitigation, choose **Enable** and then select the AWS WAF rule action that you want Shield Advanced to use in its custom rules\. Your choices are `Count` and `Block`\. For information about these actions, see [AWS WAF rule action](waf-rule-action.md)\.
   + To disable automatic mitigation, choose **Disable**\. 
   + To leave the automatic mitigation settings unchanged for the resources that you're managing, leave the default choice **Keep current settings**\. 

   For information about Shield Advanced automatic application layer DDoS mitigation, see [Shield Advanced automatic application layer DDoS mitigation](ddos-automatic-app-layer-response.md)\.

1. Choose **Next**\. 

### Create alarms and notifications<a name="add-alarm-ddos"></a>

The following procedure shows how to manage CloudWatch alarms for protected resources\. 

**Note**  
CloudWatch incurs additional costs\. For CloudWatch pricing, see [Amazon CloudWatch Pricing](http://aws.amazon.com/cloudwatch/pricing/)\.

**To create alarms and notifications**

1. In the protections page **Create alarms and notifications \- *optional***, configure the SNS topics for the alarms and notifications that you want to receive\. For resources that you don't want notifications for, choose **No topic**\. You can add an Amazon SNS topic or create a new topic\. 

1. To create an Amazon SNS topic, follow these steps:

   1. In the dropdown list, choose **Create an SNS topic**\.

   1. Enter a topic name\. 

   1. Optionally enter an email address that the Amazon SNS messages will be sent to, and then choose **Add email**\. You can enter more than one\.

   1. Choose **Create**\.

1. Choose **Next**\.

## Removing AWS Shield Advanced protection from an AWS resource<a name="remove-protection"></a>

You can remove AWS Shield Advanced protection from any of your AWS resources at any time\. 

**Important**  
Deleting an AWS resource doesn't remove the resource from AWS Shield Advanced\. You must also remove the protection on the resource from AWS Shield Advanced, as described in this procedure\.

**Remove AWS Shield Advanced protection from an AWS resource**

1. Sign in to the AWS Management Console and open the AWS WAF & Shield console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the AWS Shield navigation pane, choose **Protected resources**\.

1. In the **Protections** tab, select the resources whose protections you want to remove\. 

1. Choose **Delete protections**\.

   1. If you have an Amazon CloudWatch alarm configured for a protection, you are given the option to delete the alarm along with the protection\. If you choose not to delete the alarm at this point, you can instead delete it later using the CloudWatch console\.
**Note**  
For protections that have an Amazon Route 53 health check configured, if you add the protection again later, the protection still includes the health check\. 

The preceding steps remove AWS Shield Advanced protection from specific AWS resources\. They don't cancel your AWS Shield Advanced subscription\. You will continue to be charged for the service\. For information about your AWS Shield Advanced subscription, contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.

### Removing a CloudWatch alarm from your Shield Advanced protections<a name="remove-cloudwatch-ddos"></a>

To remove a CloudWatch alarm from your Shield Advanced protections, do one of the following:
+ Delete the protection as described in [Removing AWS Shield Advanced protection from an AWS resource](#remove-protection)\. Be sure to select the check box next to **Also delete related DDoSDetection alarm**\.
+ Delete the alarm using the CloudWatch console\. The name of the alarm to delete starts with **DDoSDetectedAlarmForProtection**\.