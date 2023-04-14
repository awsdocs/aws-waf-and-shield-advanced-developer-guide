# Version management with managed rule groups<a name="waf-managed-rule-groups-versioning"></a>

Many managed rule group providers update a rule group's options and capabilities in new versions of the rule group\. Usually, a specific version of a managed rule group is static\. Occasionally, a provider might need to update some or all of their existing versions of a managed rule group, for example, to respond to an emerging security threat\. 

When you add a managed rule group to your web ACL, if the rule group supports versioning, you can choose to let the provider manage which version you use or you can manage the version setting yourself\. 

**Can't find the version you want?**  
If you don't see a version in a rule group's version listing, the version is probably scheduled for expiration or already expired\. After a version is scheduled for expiration, AWS WAF no longer lets you to choose it for the rule group\. 

**Versioning and SNS notifications for AWS Managed Rules rule groups**  
The AWS Managed Rules rule groups all provide versioning and SNS update notifications except for the rule groups for IP reputation, Bot Control, and account takeover prevention\. 

The AWS Managed Rules rule groups that provide notifications all use the same SNS topic Amazon Resource Name \(ARN\)\.

**Topics**
+ [Version lifecycle for managed rule groups](#waf-managed-rule-groups-versioning-lifecycle)
+ [Best practices for handling managed rule group versions](#waf-managed-rule-groups-best-practice)

## Version lifecycle for managed rule groups<a name="waf-managed-rule-groups-versioning-lifecycle"></a>

Providers handle the following lifecycle stages of a managed rule group static version: 
+ **Release and updates** – A managed rule group provider announces upcoming and new static versions of their managed rule groups through notifications to an Amazon Simple Notification Service \(Amazon SNS\) topic\. Providers might also use the topic to communicate other important information about their rule groups, such as urgent required updates\. 

  You can subscribe to the rule group's topic and configure how you want to receive notifications\. For more information see [Getting notified of new versions and updates](waf-using-managed-rule-groups-sns-topic.md)\.
+ **Expiration scheduling** – A managed rule group provider schedules older versions of a rule group for expiration\. A version that's scheduled to expire cannot be added to your web ACL rules\. After expiration is scheduled for a version, AWS WAF tracks the expiration with a countdown metric in Amazon CloudWatch\. 

  You can set an alarm on the metric in CloudWatch to track the expiration of a version that you're using\. This gives you time to test a new version and move off of the expiring one before the countdown completes\. For more information, see [Tracking version expiration](waf-using-managed-rule-groups-expiration.md)\.
+ **Version expiration** – When a version expires, the rule group provider determines how to manage the expiration for web ACLs that are still using the expired version:
  + For AWS Managed Rules rule groups, AWS WAF moves any web ACL that's using the expired version to the rule group's default version\. 
  + For AWS Marketplace rule groups, the provider determines how to handle the expiration\. Ask your managed rule group provider for information\. 

## Best practices for handling managed rule group versions<a name="waf-managed-rule-groups-best-practice"></a>

Follow this versioning best practice guidance when you use a managed rule group\.

When you use a managed rule group in your web ACL, you can choose to use a specific, static version of the rule group, or you can choose to use the default version: 
+ **Default version** – AWS WAF always sets the default version to the static version that's currently recommended by the provider\. When the provider updates their recommended static version, AWS WAF automatically updates the default version setting for the rule group in your web ACL\. 

  When you use the default version of a managed rule group, do the following as best practice: 
  + **Subscribe to notifications** – Subscribe to notifications for changes to the rule group and keep an eye on those\. Most providers send advanced notification of new static versions and of default version changes\. These let you check the effects of a new static version before AWS switches the default version to it\. For more information see [Getting notified of new versions and updates](waf-using-managed-rule-groups-sns-topic.md)\.
  + **Review the effects of static version settings and make adjustments as needed before your default is set to it** – Before your default is set to a new static version, review the effects of the static version on the monitoring and management of your web requests\. The new static version might have new rules to review\. Look for false positives or other unexpected behavior, in case you need to modify how you use the rule group\. You can set rules to count, for example, to stop them from blocking traffic while you figure out how you want to handle the new behavior\. For more information, see [Testing and tuning your AWS WAF protections](web-acl-testing.md)\.
+ **Static version** – If you choose to use a static version, you must manually update the version setting when you're ready to adopt a new version of the rule group\. 

  When you use a static version of a managed rule group, do the following as best practice: 
  + **Keep your version up to date** – Keep your managed rule group as close as you can to the latest version\. When a new version is released, test it, adjust settings as needed, and implement it in a timely manner\. For information about testing, see [Testing and tuning your AWS WAF protections](web-acl-testing.md)\.
  + **Subscribe to notifications** – Subscribe to notifications for changes to the rule group, so you know when your provider releases new static versions\. Most providers give advanced notification of version changes\. Additionally, your provider might need to update the static version that you're using to close a security loophole or for other urgent reasons\. You'll know what's happening if you're subscribed to the provider's notifications\. For more information, see [Getting notified of new versions and updates](waf-using-managed-rule-groups-sns-topic.md)\.
  + **Avoid version expiration** – Don't allow a static version to expire while you're using it\. Provider handling of expired versions can vary and might include forcing an upgrade to an available version or other changes that can have unexpected consequences\. Track the AWS WAF expiry metric and set an alarm that gives you a sufficient number of days to successfully upgrade to a supported version\. For more information, see [Tracking version expiration](waf-using-managed-rule-groups-expiration.md)\.