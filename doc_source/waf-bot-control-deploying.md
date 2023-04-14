# Testing and deploying AWS WAF Bot Control<a name="waf-bot-control-deploying"></a>

This section provides general guidance for configuring and testing an AWS WAF Bot Control implementation for your site\. The specific steps that you choose to follow will depend on your needs, resources, and the web requests that you receive\. 

This information is in addition to the general information about testing and tuning provided at [Testing and tuning your AWS WAF protections](web-acl-testing.md)\.

**Note**  
AWS Managed Rules are designed to protect you from common web threats\. When used in accordance with the documentation, AWS Managed Rules rule groups add another layer of security for your applications\. However, AWS Managed Rules rule groups aren't intended as a replacement for your security responsibilities, which are determined by the AWS resources that you select\. Refer to the [Shared Responsibility Model](https://aws.amazon.com/compliance/shared-responsibility-model/) to ensure that your resources in AWS are properly protected\. 

**Production traffic risk**  
Before you deploy your Bot Control implementation for production traffic, test and tune it in a staging or testing environment until you are comfortable with the potential impact to your traffic\. Then test and tune the rules in count mode with your production traffic before enabling them\. 

This guidance is intended for users who know generally how to create and manage AWS WAF web ACLs, rules, and rule groups\. Those topics are covered in prior sections of this guide\. 

**To configure and test a Bot Control implementation**

Perform these steps first in a test environment, then in production\.

1. 

**Add the Bot Control managed rule group**
**Note**  
You are charged additional fees when you use this managed rule group\. For more information, see [AWS WAF Pricing](http://aws.amazon.com/waf/pricing/)\.

   Add the managed AWS rule group `AWSManagedRulesBotControlRuleSet` to a new or existing web ACL and configure it so that it doesn't alter current web ACL behavior\. 
   + When you add the managed rule group, edit it and do the following: 
     + In the **Inspection level** pane, select the inspection level that you want to use\. 
       + **Common** – Detects a variety of self\-identifying bots, such as web scraping frameworks, search engines, and automated browsers\. Bot Control protections at this level identify common bots using traditional bot detection techniques, such as static request data analysis\. The rules label traffic from these bots and block the ones that they cannot verify\. 
       + **Targeted** – Includes the common\-level protections and adds detection for advanced bots that do not self identify\. Targeted protections use advanced detection techniques such as browser interrogation, fingerprinting, and behavior heuristics to identify bad bot traffic\. The protections target these bots using a combination of rate limiting and CAPTCHA and background browser challenges\. The rules that provide targeted protection have names that begin with `TGT_`\.

       For more information about this choice, see [AWS WAF Bot Control rule group](aws-managed-rule-groups-bot.md)\.
     + In the **Rules** pane, open the **Override all rule actions** dropdown and choose **Count**\. With this configuration, AWS WAF evaluates requests against all of the rules in the rule group and only counts the matches that result, while still adding labels to requests\. For more information, see [Overriding rule actions in a rule group](web-acl-rule-group-settings.md#web-acl-rule-group-rule-action-override)\.

       With this override, you can monitor the potential impact of the Bot Control rules on your traffic, to determine whether you want to add exceptions for things like internal use cases or desired bots\. 
   + Position the rule group so that it's evaluated last in the web ACL, with a priority setting that's numerically higher than any other rules or rule groups that you're already using\. For more information, see [Processing order of rules and rule groups in a web ACL](web-acl-processing-order.md)\. 

     This way, your current handling of traffic isn't disrupted\. For example, if you have rules that detect malicious traffic such as SQL injection or cross\-site scripting, they'll continue to detect and log those requests\. Alternately, if you have rules that allow known non\-malicious traffic, they can continue to allow that traffic, without having it blocked by the Bot Control managed rule group\. You might decide to adjust the processing order during your testing and tuning activities, but this is a good way to start\.

1. 

**Enable sampling, logging, and metrics for the web ACL**

   As needed, configure logging for the web ACL, and enable sampling and Amazon CloudWatch metrics\. You can use metrics and logging to monitor the interaction of your web traffic with the Bot Control managed rule group\. 
   + For information about configuring and using logging, see [Logging web ACL traffic](logging.md)\. 
   + For information about Amazon CloudWatch metrics, see [Monitoring with Amazon CloudWatch](monitoring-cloudwatch.md)\. 
   + For information about web request sampling, see [Viewing a sample of web requests](web-acl-testing-view-sample.md)\. 

1. 

**Associate the web ACL with a resource**

   If the web ACL isn't already associated with a resource, associate it\. For information, see [Associating or disassociating a web ACL with an AWS resource](web-acl-associating-aws-resource.md)\.

1. 

**Monitor traffic and Bot Control rule matches**

   Make sure that traffic is flowing and that the Bot Control managed rule group rules are adding labels to matching web requests\. You can see the labels in the logs and see bot and label metrics in the Amazon CloudWatch metrics\. In the logs, the rules that you've overridden to count in the rule group show up in the `ruleGroupList` with `action` set to count, and with `overriddenAction` indicating the configured rule action that you overrode\.
**Note**  
The Bot Control managed rule group verifies bots using the IP addresses from AWS WAF\. If you use Bot Control and you have verified bots that route through a proxy or load balancer, you might need to explicitly allow them using a custom rule\. For information about how to create a custom rule, see [Forwarded IP address](waf-rule-statement-forwarded-ip-address.md)\. For information about how you can use the rule to customize Bot Control web request handling, see the next step\. 

   Carefully review the web request handling for any false positives that you might need to mitigate with custom handling\. For examples of false positives, see [False positives with AWS WAF Bot Control](waf-bot-control-false-positives.md)\.

1. 

**Customize Bot Control web request handling**

   As needed, add your own rules that explicitly allow or block requests, to change how Bot Control rules would otherwise handle them\. 

   How you do this depends on your use case, but the following are common solutions:
   + Explicitly allow requests with a rule that you add before the Bot Control managed rule group\. With this, the allowed requests never reach the rule group for evaluation\. This can help contain the cost of using the Bot Control managed rule group\. 
   + Exclude requests from Bot Control evaluation by adding a scope\-down statement inside the Bot Control managed rule group statement\. This functions the same as the preceding option\. It can help contain the cost of using the Bot Control managed rule group because the requests that don't match the scope\-down statement never reach rule group evaluation\. For information about scope\-down statements, see [Scope\-down statements](waf-rule-scope-down-statements.md)\. 

     For examples, see the following: 
     + [Exclude IP range from bot management](waf-bot-control-example-scope-down-ip.md)
     + [Allow traffic from a bot that you control](waf-bot-control-example-scope-down-your-bot.md)
   + Use Bot Control labels in request handling to allow or block requests\. Add a label match rule after the Bot Control managed rule group to filter out labeled requests that you want to allow from those that you want to block\. 

     After testing, keep the related Bot Control rules in count mode, and maintain the request handling decisions in your custom rule\. For information about label match statements, see [Label match rule statement](waf-rule-statement-type-label-match.md)\. 

     For examples of this type of customization, see the following: 
     + [Create an exception for a blocked user agent](waf-bot-control-example-user-agent-exception.md)
     + [Allow a specific blocked bot](waf-bot-control-example-allow-blocked-bot.md)
     + [Block verified bots](waf-bot-control-example-block-verified-bots.md)

   For additional examples, see [AWS WAF Bot Control examples](waf-bot-control-examples.md)\.

1. 

**As needed, enable the Bot Control managed rule group settings**

   Depending on your situation, you might have decided that you want to leave some Bot Control rules in count mode or with a different action override\. For the rules that you want to have run as they are configured inside the rule group, enable the regular rule configuration\. To do this, edit the rule group statement in your web ACL and make your changes in the **Rules** pane\. 