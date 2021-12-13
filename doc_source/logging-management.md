# Managing logging for a web ACL<a name="logging-management"></a>

You can enable and disable logging for a web ACL at any time\.

In the logging configuration for your web ACL, you can customize what AWS WAF sends to the logs\.
+ **Field redaction** – You can redact some fields from the log records\. Redacted fields appear as `XXX` in the logs\. For example, if you redact the **URI** field, the **URI** field in the logs will be `XXX`\. For a list of the log fields, see [Log Fields](logging-fields.md)\.
+ **Log filtering** – You can add filtering to specify which web requests are kept in the logs and which are dropped\. You can filter on the rule action and on the web request labels that were applied during the request evaluation\. For information about rule action settings, see [AWS WAF rule action](waf-rule-action.md)\. For information about labels, see [AWS WAF labels on web requests](waf-rule-labels.md)\.<a name="logging-procedure"></a>

**To enable logging for a web ACL**

This procedure requires a configured logging destination\. For information about your destination choices and the requirements for each, see [AWS WAF logging destinations](logging-destinations.md)\.

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Web ACLs**\.

1. Choose the web ACL that you want to enable logging for\.

1. On the **Logging** tab, choose **Enable logging**\.

1. Choose the logging destination type, and then choose the logging destination that you configured\. You must choose a logging destination whose name begins with `aws-waf-logs-`\.

1. \(Optional\) If you don't want certain fields and their values included in the logs, redact those fields\. Choose the field to redact, and then choose **Add**\. Repeat as necessary to redact additional fields\. The redacted fields appear as `XXX` in the logs\. For example, if you redact the **URI** field, the **URI** field in the logs will be `XXX`\. 

1. \(Optional\) If you don't want to send all requests to the logs, add your filtering criteria and behavior\. Under **Filter logs**, for each filter that you want to apply, choose **Add filter**, then choose your filtering criteria and specify whether you want to keep or drop requests that match the criteria\. When you finish adding filters, if needed, modify the **Default logging behavior**\. 

1. Choose **Enable logging**\.
**Note**  
When you successfully enable logging, AWS WAF will create a service linked role with the necessary permissions to write logs to the logging destination\. For more information, see [Using service\-linked roles for AWS WAF](using-service-linked-roles.md)\.

**To disable logging for a web ACL**

1. In the navigation pane, choose **Web ACLs**\.

1. Choose the web ACL that you want to disable logging for\.

1. On the **Logging** tab, choose **Disable logging**\.

1. In the dialog box, choose **Disable logging**\.