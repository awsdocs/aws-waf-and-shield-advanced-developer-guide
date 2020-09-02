# AWS WAF policies<a name="waf-policies"></a>

A Firewall Manager AWS WAF policy contains the rule groups that you want to apply to your resources\. When you apply the policy, Firewall Manager creates a Firewall Manager web ACL in each account that's within policy scope\. Then, the individual account managers can add rules and rule groups to the resulting web ACL, in addition to the rule groups that you have defined\. 

## Rule groups in AWS Firewall Manager AWS WAF policies<a name="waf-policies-rule-groups"></a>

The web ACLs that are managed by Firewall Manager AWS WAF policies contain three sets of rules\. These sets provide a higher level of prioritization for the rules and rule groups in the web ACL: 
+ First rule groups, defined by you in the Firewall Manager AWS WAF policy\. AWS WAF evaluates these rule groups first\.
+ Rules and rule groups that are defined by the account managers in the web ACLs\. AWS WAF evaluates any account\-managed rules or rule groups next\. 
+ Last rule groups, defined by you in the Firewall Manager AWS WAF policy\. AWS WAF evaluates these rule groups last\.

Within each of these sets of rules, AWS WAF evaluates rules and rule groups as usual, according to their priority settings within the set\.

In the policy's first and last rule groups sets, you can only add rule groups\. You can use managed rule groups, which AWS Managed Rules and AWS Marketplace sellers create and maintain for you\. You can also manage and use your own rule groups\. For more information about all of these options, see [Rule groups](waf-rule-groups.md)\.

If you want to use your own rule groups, you create those before you create your Firewall Manager AWS WAF policy\. For guidance, see [Managing your own rule groups](waf-user-created-rule-groups.md)\. To use an individual custom rule, you must define your own rule group, define your rule within that, and then use the rule group in your policy\.

For information about how AWS WAF evaluates web requests, see [How AWS WAF processes a web ACL](web-acl-processing.md)\.

For the procedure to create a Firewall Manager AWS WAF policy, see [Creating an AWS Firewall Manager policy for AWS WAF](create-policy.md#creating-firewall-manager-policy-for-waf)\.

## Configuring logging for an AWS Firewall Manager AWS WAF policy<a name="waf-policies-logging-config"></a>

You can enable centralized logging for your AWS WAF policies, to get detailed information about traffic within your organization\. Information in the logs includes the time that AWS WAF received the request from your AWS resource, detailed information about the request, and the action for the rule that each request matched from all in\-scope accounts\. For more information about AWS WAF logging, see [Logging Web ACL traffic information](logging.md)\.

**Note**  
AWS Firewall Manager supports this option for the latest version of AWS WAF, and not for AWS WAF Classic\.

When you enable centralized logging on an AWS WAF policy, Firewall Manager creates a web ACL for the policy in the Firewall Manager administrator account as follows: 
+ Firewall Manager creates the web ACL in the Firewall Manager administrator account regardless of whether the account is in scope of the policy\.
+ The web ACL has logging enabled, with a log name `FMManagedWebACLV2Logging<policy-name><timestamp>`\. The web ACL has no rule groups and no associated resources\. 
+ You are charged for the web ACL according to the AWS WAF pricing guidelines\. For more information, see [AWS WAF Pricing](http://aws.amazon.com/waf/pricing/)\. 
+ Firewall Manager deletes the web ACL when you delete the policy\. 

You send logs from your policy's web ACLs to an Amazon Kinesis Data Firehose where you've configured a storage destination\. After you enable logging, AWS WAF delivers logs for each configured web ACL, through the HTTPS endpoint of Kinesis Data Firehose to the configured storage destination\. Before you use it, test your delivery stream to be sure that it has enough throughput to accommodate your organization's logs\. For more information about how to create an Amazon Kinesis Data Firehose and review the stored logs, see [What Is Amazon Kinesis Data Firehose?](https://docs.aws.amazon.com/firehose/latest/dev/what-is-this-service.html)

You must have the following permissions to successfully enable logging:
+ `iam:CreateServiceLinkedRole`
+ `firehose:ListDeliveryStreams`
+ `wafv2:PutLoggingConfiguration`

For information about service\-linked roles and the `iam:CreateServiceLinkedRole` permission, see [Using service\-linked roles for AWS WAF](using-service-linked-roles.md)\.

**To enable logging for an AWS WAF policy**

1. Create an Amazon Kinesis Data Firehose using your Firewall Manager administrator account\. Use a name starting with the prefix `aws-waf-logs-`\. For example, `aws-waf-logs-firewall-manager-central`\. Create the data firehose with a `PUT` source and in the region that you are operating\. If you are capturing logs for Amazon CloudFront, create the firehose in US East \(N\. Virginia\)\. Before you use it, test your delivery stream to be sure that it has enough throughput to accommodate your organization's logs\. For more information, see [Creating an Amazon Kinesis Data Firehose delivery stream](https://docs.aws.amazon.com/firehose/latest/dev/basic-create.html)\.

1. Sign in to the AWS Management Console using the Firewall Manager administrator account that you set up in the prerequisites \([AWS Firewall Manager prerequisites](fms-prereq.md)\), and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 

1. In the navigation pane, choose **Security Policies**\.

1. Choose the AWS WAF policy that you want to enable logging for\.

1. On the **Policy details** tab, in the **Policy rules** section, choose **Edit**\. 

1. For **Logging configuration status**, choose **Enabled**\.

1. Choose the Kinesis Data Firehose that you created for your logging\. You must choose a firehose that begins with `aws-waf-logs-`\.

1. \(Optional\) If you don't want certain fields and their values included in the logs, redact those fields\. Choose the field to redact, and then choose **Add**\. Repeat as necessary to redact additional fields\. The redacted fields appear as `XXX` in the logs\. For example, if you redact the **URI** field, the **URI** field in the logs will be `XXX`\. 

1. Choose **Next**\.

1. Review your settings, then choose **Save** to save your changes to the policy\.

**To disable logging for an AWS WAF policy**

1. Sign in to the AWS Management Console using the Firewall Manager administrator account that you set up in the prerequisites \([AWS Firewall Manager prerequisites](fms-prereq.md)\), and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 

1. In the navigation pane, choose **Security Policies**\.

1. Choose the AWS WAF policy that you want to disable logging for\.

1. On the **Policy details** tab, in the **Policy rules** section, choose **Edit**\. 

1. For **Logging configuration status**, choose **Disabled**\.

1. Choose **Next**\.

1. Review your settings, then choose **Save** to save your changes to the policy\.