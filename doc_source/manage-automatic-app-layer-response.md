# Managing automatic application layer DDoS mitigation<a name="manage-automatic-app-layer-response"></a>

Use the guidance in this section to manage your automatic application layer DDoS mitigation configurations\. For information about how automatic mitigation works, see the preceding topics\. 

**Topics**
+ [Enabling and disabling automatic application layer DDoS mitigation](#enable-disable-automatic-app-layer-response)
+ [Changing the action used for automatic application layer DDoS mitigation](#change-action-of-automatic-app-layer-response)

## Enabling and disabling automatic application layer DDoS mitigation<a name="enable-disable-automatic-app-layer-response"></a>

The following procedure shows how to enable or disable automatic response for a protected resource\.

**To enable or disable automatic application layer DDoS mitigation**

1. Sign in to the AWS Management Console and open the AWS WAF & Shield console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the AWS Shield navigation pane, choose **Protected resources**\.

1. In the **Protections** tab, select the application layer resource that you want to enable automatic mitigation for\. The protections page opens for the resource\. 

1. In the resource's protections page, choose **Edit**\. 

1. In the page **Configure layer 7 DDoS mitigation for global resources \- *optional***, for **Automatic application layer DDoS mitigation**, select **Enable**, and then select the rule action that you want the automatic mitigations to use in the web ACL rules\. For information about the rule settings, see [AWS WAF rule action](waf-rule-action.md)\.

1. Walk through the rest of the pages until you finish and save the configuration\. 

In the **Protections** page, automatic mitigation is indicated as enabled for the resource\.

## Changing the action used for automatic application layer DDoS mitigation<a name="change-action-of-automatic-app-layer-response"></a>

You can change the action that Shield Advanced uses for its application layer automatic response in multiple locations in the console:
+ **Automatic mitigation configuration** – Change the action when you configure automatic mitigation for your resource\. For the procedure, see the preceding section [Enabling and disabling automatic application layer DDoS mitigation](#enable-disable-automatic-app-layer-response)\.
+ **Event details page** – Change the action in the event details page, when you're viewing the event information in the console\. For information, see [AWS Shield Advanced event details](ddos-event-details.md)\.