# Testing and deploying ATP<a name="waf-atp-deploying"></a>

This section provides general guidance for configuring and testing an AWS WAF Fraud Control account takeover prevention \(ATP\) implementation for your site\. The specific steps that you choose to follow will depend on your needs, resources, and web requests that you receive\. 

**Production traffic risk**  
Before you deploy your ATP implementation for production traffic, test and tune it in a staging or testing environment until you are comfortable with the potential impact to your traffic\. Then test and tune the rules in count mode with your production traffic before enabling them\. 

AWS WAF provides test credentials that you can use to verify your ATP configuration\. In the following procedure, you'll configure a test web ACL to use the ATP managed rule group, configure a rule to capture the label added by the rule group, and then run a login attempt using these test credentials\. You'll verify that your web ACL has properly managed the attempt by checking the Amazon CloudWatch metrics for the login attempt\. 

This guidance is intended for users who know generally how to create and manage AWS WAF web ACLs, rules, and rule groups\. Those topics are covered in prior sections of this guide\. 

**To configure and test an AWS WAF Fraud Control account takeover prevention \(ATP\) implementation**

Perform these steps first in a test environment, then in production\.

1. 

**Add the AWS WAF Fraud Control account takeover prevention \(ATP\) managed rule group**

   Add the AWS Managed Rules rule group `AWSManagedRulesATPRuleSet` to a new or existing web ACL and configure it so that it doesn't alter the current web ACL behavior\. For details about the rules and labels for this rule group, see [AWS WAF Fraud Control account takeover prevention \(ATP\) rule group](aws-managed-rule-groups-atp.md)\.
   + When you add the managed rule group, edit it and do the following: 
     + In the **Rule group configuration** pane, provide the details of your application's login page\. The ATP rule group uses this information to monitor sign\-in activities\. For more information, see [Using the ATP managed rule group](waf-atp-rg-using.md)\.
     + In the **Rules** pane, turn on the **Set all rule actions to count** toggle\. With this configuration, AWS WAF evaluates requests against all of the rules in the rule group and only counts the matches that result, while still adding labels to requests\. For more information, see [Setting rule actions to count in a rule group](web-acl-rule-group-settings.md#web-acl-rule-group-rule-to-count)\.

       This allows you to monitor the impact of the ATP managed rules to determine whether you want to add exceptions, such as exceptions for internal use cases\. 
   + Position the rule group so that it's evaluated after your existing rules in the web ACL, with a priority setting that's numerically higher than any rules or rule groups that you're already using\. For more information, see [Processing order of rules and rule groups in a web ACL](web-acl-processing-order.md)\. 

     This way, your current handling of traffic isn't disrupted\. For example, if you have rules that detect malicious traffic such as SQL injection or cross\-site scripting, they'll continue to detect and log that\. Alternately, if you have rules that allow known non\-malicious traffic, they can continue to allow that traffic, without having it blocked by the ATP managed rule group\. You might decide to adjust the processing order during your testing and tuning activities\.

1. 

**Add a rule to match against the ATP rule group's label for compromised credentials**

   Immediately after the ATP rule group, add a label match rule as follows: 
   + Match against the label `awswaf:managed:aws:atp:signal:credential_compromised`\. 
   + Set the rule action to `Count`\.
   + Make sure this rule has a higher numeric priority setting than the ATP rule group so that this rule runs after the ATP rules\. In the console, it should be listed last\. For more information, see [Processing order of rules and rule groups in a web ACL](web-acl-processing-order.md)\. 

   You'll look for the name of this rule in your Amazon CloudWatch metrics, when you test your configuration\. 

1. 

**Enable sampling, logging, and metrics for the web ACL**

   As needed, configure logging for the web ACL, and enable sampling and Amazon CloudWatch metrics\. This allows you to monitor the interaction of the ATP managed rule group with your traffic\. 
   + For information about configuring and using logging, see [Logging web ACL traffic](logging.md)\. 
   + For information about Amazon CloudWatch metrics, see [Monitoring with Amazon CloudWatch](monitoring-cloudwatch.md)\. 
   + For information about web request sampling, see [Viewing a sample of web requests](web-acl-testing-view-sample.md)\. 

1. 

**Associate the web ACL with a resource**

   If the web ACL isn't already associated with a test resource, associate it\. For information, see [Associating or disassociating a web ACL with an AWS resource](web-acl-associating-aws-resource.md)\.

1. 

**Monitor traffic and ATP rule matches**

   Make sure that your normal traffic is flowing and that the ATP managed rule group rules are adding labels to matching web requests\. You can see the labels in the logs and see the label match rule metrics in Amazon CloudWatch metrics\. In the logs, the rules that you've set to count in the rule group show up under `excludedRules` in the `ruleGroupList`\. 

1. 

**Test the rule group's credential checking capabilities**

   Perform a login attempt with test compromised credentials and check that the rule group matches against them as expected\. Do the following:

   1. Log in to your protected resource's login page using one of the following AWS WAF test credential pairs: 
      + User: `WAF_TEST_CREDENTIAL`, password: `WAF_TEST_CREDENTIAL_PASSWORD`
      + User: `WAF_TEST_CREDENTIAL@wafexample.com`, password: `WAF_TEST_CREDENTIAL_PASSWORD`

      These test credentials are categorized as compromised credentials, and the ATP managed rule group will add the `awswaf:managed:aws:atp:signal:credential_compromised` label to the login request\. 

   1. Check for the following results from your test: 
      + In your Amazon CloudWatch metrics, look for `CountedRequest` metrics for your rule that matches against the compromised credentials label\. For information about Amazon CloudWatch metrics, see [Monitoring with Amazon CloudWatch](monitoring-cloudwatch.md)\. 
      + In your web ACL logs, look for the `awswaf:managed:aws:atp:signal:credential_compromised` label in the `labels` field on the log entry for your test login web request\. For information about logging, see [Logging web ACL traffic](logging.md)\. 

   After you've verified that the rule group captures compromised credentials as expected, you can take steps to configure its implementation as you need for your protected resource\.

1. 

**Customize ATP web request handling**

   As needed, add your own rules that explicitly allow or block requests, to change how ATP rules would otherwise handle them\. 

   For example, you can use ATP labels to allow or block requests or to customize request handling\. You can add a label match rule after the ATP managed rule group to filter labeled requests for the handling that you want to apply\. After testing, keep the related ATP rules in count mode, and maintain the request handling decisions in your custom rule\. For an example, see [ATP example: Custom handling for missing and compromised credentials](waf-atp-control-example-user-agent-exception.md)\. 

1. 

**Remove your test rule and enable the ATP managed rule group settings**

   Depending on your situation, you might have decided that you want to leave some ATP rules in count mode\. For the rules that you want to run the way that they're configured inside the rule group, enable the regular rule configuration\. To do this, disable count mode in the web ACL rule group configuration for the rules\. When you're finished testing, you can also remove your test label match rule\.

1. 

**Monitor and tune**

   To be sure that web requests are being handled as you want, closely monitor your traffic after you enable the ATP functionality that you intend to use\. Adjust the behavior as needed with the rules count override on the rule group and with your own rules\. 

After you finish testing your ATP rule group implementation, we recommend that you integrate the AWS WAF ATP JavaScript SDK into your browser login page, for enhanced detection capabilities\. AWS WAF also provides mobile SDKs to integrate iOS and Android devices\. For more information about the integration SDKs, see [AWS WAF client application integration](waf-application-integration.md)\. 