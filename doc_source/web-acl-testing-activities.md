# Monitoring and tuning<a name="web-acl-testing-activities"></a>

This section describes how to monitor and tune your AWS WAF protections\. 

**Note**  
To follow the guidance in this section, you need to understand generally how to create and manage AWS WAF protections like web ACLs, rules, and rule groups\. That information is covered in earlier sections of this guide\.

Monitor web traffic and rule matches to verify the behavior of the web ACL\. If you find problems, adjust your rules to correct and then monitor to verify the adjustments\. 

Repeat the following procedure until the web ACL is managing your web traffic as you need it to\. 

**To monitor and tune**

1. 

**Monitor traffic and rule matches**

   Make sure that traffic is flowing and that your test rules are finding matching requests\. 

   Look for the following information for the protections that you're testing: 
   + **Logs** – In the logs, the test rules that match a web request appear as follows: 
     + Rules in the web ACL that have `Count` action are listed as `nonTerminatingMatchingRules`\.
     + Rule groups are identified in the `ruleGroupId` field\.
     + Rule group rules that you've set to `Count` through your web ACL configuration show up as `excludedRules` in the `ruleGroupList`\.
     + Labels that rules have applied to the request are listed in the `Labels` field\.

     For more information about logging contents, see [Log Fields](logging-fields.md)\.
   + **Metrics** – Metrics for the test rules that match a web request appear as follows: 
     + Rules in the web ACL that have `Count` action are listed as `Count` metrics for the web ACL\. 
     + For your rule groups, rules that you've set to `Count` through your web ACL configuration are listed under the rule group metrics\. 
**Note**  
AWS WAF doesn't generate metrics for rules that are configured with `Count` action in the rule group configuration\. It only generates metrics for rules that you override to `Count` through your web ACL configuration of the rule group reference statement\. 
     + For managed rule groups, rules that you've set to `Count` through your web ACL configuration are listed under the web ACL metrics\. Only the rule group owner can see rule group metrics\. 

     For more information about metrics, see [Viewing metrics for your web ACL](web-acl-testing-view-metrics.md)\.
   + **Sampled web requests** – Sampled requests provide information for the test rules that match the web request as follows: 
     + The sample information identifies matching rules by the metric name for the rule in the web ACL\. For rule groups, the metric identifies the rule group reference statement\. 
     + For rules inside rule groups, the sample lists the matching rule name in `RuleWithinRuleGroup`\. 

     For more about request samples, see [Viewing a sample of web requests](web-acl-testing-view-sample.md)\.

1. 

**Configure mitigations to address false positives**

   If you determine that a rule is generating false positives, by matching web requests when it shouldn't, the following options can help you tune your web ACL protections to mitigate\. 

**Correcting rule inspection criteria**  
For your own rules, you often just need to adjust the settings that you're using to inspect web requests\. Examples include changing the specifications in a regex pattern set, adjusting the text transformations that you apply to a request component before inspection, or switching to using a forwarded IP address\. See the guidance for the rule type that's causing problems, under [AWS WAF rule statements](waf-rule-statements.md)\. 

**Correcting more complex problems**  
For inspection criteria that you don't control and for some complex rules, you might need to make other changes, like adding rules that explicitly allow or block requests or that eliminate requests from evaluation by the problematic rule\. Managed rule groups most commonly need this type of mitigation, but other rules can too\. Examples include the rate\-based rule statement and the SQL injection attack rule statement\. 

   What you do to mitigate false positives depends on your use case\. The following are common approaches:
   + **Add a mitigating rule** – Add a rule that runs before the new rule and that explicitly allows requests that are causing false positives\. For information about rule evaluation order in a web ACL, see [Processing order of rules and rule groups in a web ACL](web-acl-processing-order.md)\.

     With this approach, the allowed requests are sent to the protected resource, so they never reach the new rule for evaluation\. If the new rule is a paid managed rule group, this approach can also help contain the cost of using the rule group\. 
   + **Add a logical rule with a mitigating rule** – Use logical rule statements to combine the new rule with a rule that excludes the false positives\. Logical rule statements are listed under [Rule statements list](waf-rule-statements-list.md)\.

     For example, say you're adding an SQL injection attack match statement that's generating false positives for a category of requests\. Create a rule that matches those requests, and then combine the rules using logical rule statements so that you match only on requests that don't match the false positives criteria and do match the SQL injection attack criteria\. 
   + **Add a scope\-down statement** – For rate\-based statements and managed rule group reference statements, exclude requests that result in false positives from evaluation by adding a scope\-down statement inside the main statement\. 

     A request that doesn't match the scope\-down statement never reaches the rule group or rate\-based evaluation\. For information about scope\-down statements, see [Scope\-down statements](waf-rule-scope-down-statements.md)\. For an example, see [Exclude IP range from bot management](waf-bot-control-example-scope-down-ip.md)\. 
   + **Add a label match rule** – For rule groups that use labeling, identify the label that the problematic rule is applying to requests\. Add a label match rule, positioned to run after the rule group, that matches against the identified label\. In the label match rule, you can filter the requests that you want to allow from those that you want to block\. 

     If you use this approach, when you're finished testing, keep the problematic rule in count mode in the rule group, and keep your custom label match rule in place\. For information about label match statements, see [Label match rule statement](waf-rule-statement-type-label-match.md)\. For examples, see [Allow a specific blocked bot](waf-bot-control-example-allow-blocked-bot.md) and [ATP example: Custom handling for missing and compromised credentials](waf-atp-control-example-user-agent-exception.md)\. 
   + **Change the version of a managed rule group** – For versioned managed rule groups, change the version that you're using\. For example, you could switch back to the last static version that you were using successfully\. 

     This is usually a temporary fix\. You might change the version for your production traffic while you continue testing the latest version in your test or staging environment, or while you wait for a more compatible version from the provider\. For information about managed rule group versions, see [Managed rule groups](waf-managed-rule-groups.md)\.

When you're satisfied that the new rules are matching requests as you need them to, move to the next stage of your testing and repeat this procedure\. The final stage of testing and tuning should be in your production environment\.