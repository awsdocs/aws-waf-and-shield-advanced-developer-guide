# Managing automatic application layer DDoS mitigation<a name="manage-automatic-app-layer-response"></a>

Use the guidance in this section to manage your automatic application layer DDoS mitigation configurations\. For information about how automatic mitigation works, see the preceding topics\. 

**Topics**
+ [Viewing the automatic application layer DDoS mitigation configuration for a resource](#view-automatic-app-layer-response-configuration)
+ [Enabling and disabling automatic application layer DDoS mitigation](#enable-disable-automatic-app-layer-response)
+ [Changing the action used for automatic application layer DDoS mitigation](#change-action-of-automatic-app-layer-response)

## Viewing the automatic application layer DDoS mitigation configuration for a resource<a name="view-automatic-app-layer-response-configuration"></a>

You can view the automatic application layer DDoS mitigation configuration for a resource in the **Protected resources** page and in the individual protections pages\. 

**To view the automatic application layer DDoS mitigation configuration**

1. Sign in to the AWS Management Console and open the AWS WAF & Shield console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the AWS Shield navigation pane, choose **Protected resources**\. In the list of protected resources, the column **Automatic application layer DDoS mitigation** indicates whether automatic mitigation is enabled and, where enabled, the action that Shield Advanced is to use in its mitigations\. 

   You can also select any application layer resource to see the same information listed on the protections page for the resource\. 

## Enabling and disabling automatic application layer DDoS mitigation<a name="enable-disable-automatic-app-layer-response"></a>

The following procedure shows how to enable or disable automatic response for a protected resource\. 

**To enable or disable automatic application layer DDoS mitigation for a single resource**

1. Sign in to the AWS Management Console and open the AWS WAF & Shield console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the AWS Shield navigation pane, choose **Protected resources**\.

1. In the **Protections** tab, select the application layer resource that you want to enable automatic mitigation for\. The protections page opens for the resource\. 

1. In the resource's protections page, choose **Edit**\. 

1. In the page **Configure layer 7 DDoS mitigation for global resources \- *optional***, for **Automatic application layer DDoS mitigation**, choose the option that you want to use for automatic mitigations\. The options in the console are the following: 
   + **Keep current settings** – Make no changes to the automatic mitigation settings of the protected resource\. 
   + **Enable** – Enable automatic mitigation for the protected resource\. When you choose this, also select the rule action that you want the automatic mitigations to use in the web ACL rules\. For information about the rule action settings, see [AWS WAF rule action](waf-rule-action.md)\.
   + **Disable** – Disable automatic mitigation for the protected resource\. 

1. Walk through the rest of the pages until you finish and save the configuration\. 

In the **Protections** page, the automatic mitigation settings are updated for the resource\.

## Changing the action used for automatic application layer DDoS mitigation<a name="change-action-of-automatic-app-layer-response"></a>

You can change the action that Shield Advanced uses for its application layer automatic response in multiple locations in the console:
+ **Automatic mitigation configuration** – Change the action when you configure automatic mitigation for your resource\. For the procedure, see the preceding section [Enabling and disabling automatic application layer DDoS mitigation](#enable-disable-automatic-app-layer-response)\.
+ **Event details page** – Change the action in the event details page, when you're viewing the event information in the console\. For information, see [AWS Shield Advanced event details](ddos-event-details.md)\.