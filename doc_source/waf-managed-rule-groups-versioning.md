# Version management with managed rule groups<a name="waf-managed-rule-groups-versioning"></a>

A managed rule group provider updates a rule group's options and capabilities in new versions of the rule group\. Usually, a specific version of a managed rule group is static\. Occasionally, a provider might need to update some or all of their existing versions of a managed rule group, for example, to respond to an emerging security threat\. 

When you add a managed rule group to your web ACL, if the rule group supports versioning, you can choose to let the provider manage which version you use or you can manage the version setting yourself\. 

**Topics**
+ [Version lifecycle for managed rule groups](#waf-managed-rule-groups-versioning-lifecycle)
+ [Best practices for handling managed rule group versions](#waf-managed-rule-groups-best-practice)

## Version lifecycle for managed rule groups<a name="waf-managed-rule-groups-versioning-lifecycle"></a>

Providers handle the following lifecycle stages of a managed rule group version: 
+ **Release and updates** – A managed rule group provider announces upcoming and new versions of a managed rule group through notifications to an Amazon Simple Notification Service \(Amazon SNS\) topic\. Providers might also use the topic to communicate other important information about the rule group, such as urgent required updates\. 

  You can subscribe to the rule group's topic and configure how you want to receive notifications\. For more information see [Getting notified of new versions and updates](waf-using-managed-rule-groups-sns-topic.md)\.
+ **Expiration scheduling** – A managed rule group provider schedules older versions of a rule group for expiration\. A version that's scheduled to expire cannot be added to your web ACL rules\. After expiration is scheduled for a version, AWS WAF tracks the expiration with a countdown metric in Amazon CloudWatch\. 

  You can set an alarm on the metric in CloudWatch to track the expiration of a version that you're using\. This gives you time to test a new version and move off of the expiring one before the countdown completes\. For more information, see [Tracking version expiration](waf-using-managed-rule-groups-expiration.md)\.
+ **Version expiration** – When a version expires, the rule group provider determines how to manage the expiration for web ACLs that are still using the expired version:
  + For AWS Managed Rules rule groups, AWS WAF moves any web ACL that's using the expired version to the rule group's default version\. 
  + For AWS Marketplace rule groups, the provider determines how to handle the expiration\. Ask your managed rule group provider for information\. 

## Best practices for handling managed rule group versions<a name="waf-managed-rule-groups-best-practice"></a>

Follow this versioning best practice guidance when you use a managed rule group\.

When you use a managed rule group in your web ACL, you can choose to use a specific, static version of the rule group, or you can choose to use the default version: 
+ **Default version** – If you choose the default version, AWS WAF always uses the version that's currently recommended by the provider\. When the provider updates their recommended version, AWS WAF automatically updates the version for the rule group in your web ACL\.

  When you use the default version of a managed rule group, do the following as best practice: 
  + **Subscribe to notifications** – Subscribe to notifications for changes to the rule group and keep an eye on those\. Most providers provide advanced notification of version changes so that you can make plans to check the effects of a new version when it's released\. You'll also receive notification at the time that a new version is released\. For more information see [Getting notified of new versions and updates](waf-using-managed-rule-groups-sns-topic.md)\.
  + **Review the effects of new versions and make adjustments** – When a rule group version changes, review the effects of the new version on your web request monitoring and management\. The new version might have new rules to review\. Look for false positives or other unexpected behavior, in case you need to modify how you use the rule group\. You can set rules to count, for example, to stop them from blocking traffic while you figure out how you want to handle the new behavior\. 
+ **Static version** – If you choose to use a static version, you must manually update the version setting when you're ready to adopt a new version of the rule group\. 

  When you use a static version of a managed rule group, do the following as best practice: 
  + **Keep your version up to date** – Keep your managed rule group as close as you can to the latest version\. The latest version of any rule group contains the provider's best approach to protecting your resources\. When a new version is released, test it, adjust settings as needed, and implement it in a timely manner\. 
  + **Subscribe to notifications** – Subscribe to notifications for changes to the rule group, so you know when your provider releases new versions\. Most providers give advanced notification of version changes\. Additionally, your provider might need to update the rule group version you're using to close a security loophole or for other urgent reasons\. You'll know what's happening if you're subscribed to the provider's notifications\. For more information, see [Getting notified of new versions and updates](waf-using-managed-rule-groups-sns-topic.md)\.
  + **Avoid version expiration** – Don't allow a version to expire while you're using it\. Provider handling of expired versions can vary and might include forcing an upgrade to an available version or other changes that can have unexpected consequences\. Track the AWS WAF expiry metric and set an alarm that gives you a sufficient number of days to successfully upgrade to a supported version\. For more information, see [Tracking version expiration](waf-using-managed-rule-groups-expiration.md)\.