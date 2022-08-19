# Tracking a rule group's version expiration<a name="waf-using-managed-rule-groups-expiration"></a>

If you use a specific version of a rule group, make sure that you don't keep using a version past its expiration date\. 

**Tip**  
If you track upcoming changes for the managed rule group through Amazon SNS, you'll receive notifications about new and recommended versions\. If you regularly test and move to a newer version, you'll stay ahead of any expiration activities on the older versions\. You'll also benefit from the most current protections from the rule group\. For information about notifications, see [Getting notified of new versions and updates](waf-using-managed-rule-groups-sns-topic.md)\.

If a version that you're using is expired, AWS WAF blocks modifications to the web ACL where you're using the rule group\. The block remains until you update the rule group to an available version or remove it from your web ACL\. 

Expiration handling for a managed rule group depends on the rule group provider\. For AWS Managed Rules rule groups, the version is automatically changed to the rule group's default version\. For AWS Marketplace rule groups, ask the provider how they handle expiration\.

To monitor expiration scheduling for a managed rule group, track the Amazon CloudWatch expiry metrics from AWS WAF: 
+ Metric name: `DaysToExpiry`
+ Metric dimensions: `Region`, `ManagedRuleGroup`, `Vendor`, and `Version`

Locate the metric for your managed rule group in Amazon CloudWatch and set an alarm on it so that you're notified in time to switch to a newer version of your rule group\. For information about using Amazon CloudWatch metrics and configuring alarms, see the [Amazon CloudWatch User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/)\. 

When the provider creates a new version of the rule group, it sets the version's forecasted lifetime\. While the version isn't scheduled to expire, the metric value is set to the forecasted lifetime setting, and in CloudWatch, you'll see a flat value for the metric\. After the provider schedules the metric to expire, the metric value diminishes each day until it reaches zero on the day of expiration\. 

If you have a managed rule group in your web ACL that's evaluating traffic, you will get a metric for it\. The metric isn't available for unused rule groups\.