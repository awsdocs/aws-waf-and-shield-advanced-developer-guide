# Overriding the actions of a rule group or its rules<a name="web-acl-rule-group-override-options"></a>

When you add a rule group to your web ACL, you can alter how it manages your web requests, so that it counts matching requests rather than acting on them\. This can be useful for activities like testing and monitoring a rule group's behavior before you use it\. Doing this doesn't alter the rule group itself\. It only alters how AWS WAF uses the rule group in the context of the web ACL\. 

## Setting the rule actions to count<a name="web-acl-rule-group-override-options-rules"></a>

You can override the actions of the rules inside a managed rule group, setting them to count for some or all of the rules\. If a rule's action is configured inside the rule group to block or allow matching requests, this override changes that behavior so that matching requests are only counted\.  

This allows all of the rules in the rule group to run and generate logs and metrics without affecting how the web request is handled and without terminating the evaluation of the web request\. 

When AWS WAF evaluates a web request against a rule group whose rules are all set to count by the web ACL, if the request matches one of the rules, AWS WAF processes the match normally and then continues evaluating the subsequent rules in the rule group\. The count action is non\-terminating and doesn't prompt a match response from the rule group in the web ACL\. 

You can use this option to test a rule group or inspect it for false positives\. It allows AWS WAF to evaluate web requests against all rules in the rule group and report all matches that it finds to your configured samples, metrics, and logs\. 

This can help you troubleshoot false positives, which is when a rule group blocks traffic that you aren't expecting it to block\. If you identify a rule within the rule group that's blocking requests that you want to allow through, you can leave that rule in count mode, to exclude it from acting on your requests\.

If you want to test a rule before you start using it to allow or block requests, configure AWS WAF to count the web requests that match the conditions in the rule\. If you have metrics enabled, you'll receive `COUNT` metrics for the rule whose action is set to count\. For more information, see [Testing web ACLs](web-acl-testing.md)\.

For information about how to use this option, see [Setting rule actions to count in a rule group](web-acl-rule-group-settings.md#web-acl-rule-group-rule-to-count)\.

## Overriding the resulting rule group's action to count<a name="web-acl-rule-group-override-options-rule-group"></a>

You can override the action that the rule group returns to count\. 

When you override the rule group action to count, the allow and block actions affect the processing of the rules inside the rule group as described at [Basic handling of the rule and rule group actions in a web ACLRule and rule group actions in a web ACL](web-acl-rule-actions.md), but then at the web ACL level, the action override makes the rule group resulting action a count action, and the web ACL doesn't discontinue processing\. It processes the rest of the rules in the web ACL as if the result from the rule group were a match with count action\.

With this option, the rules in the rule group run as specified by the rule group configuration\. The first rule that matches a web request and that has a rule action of allow or block terminates the rule group evaluation and returns the allow or block action for the rule group\. At this point, the web ACL override changes the returned rule group action to count and then continues processing any other rules and rule groups that are configured in the web ACL\. So, processing inside the rule group works according to the rule group's rule configurations, up to the first rule that matches and has a termination action setting\. 

If the rules in the rule group find no match for the web request, this setting has no effect\.

For information about how to use this option, see [Overriding a rule group's action to count](web-acl-rule-group-settings.md#web-acl-rule-group-action-override)\.