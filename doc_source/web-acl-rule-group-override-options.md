# Overriding the actions of a rule group or its rules<a name="web-acl-rule-group-override-options"></a>

When you add a rule group to your web ACL, you can alter how it manages your web requests, so that it counts matching requests rather than acting on them\. This can be useful for activities like testing and monitoring a rule group's behavior before you use it\. Doing this doesn't alter the rule group itself\. It only alters how AWS WAF uses the rule group in the context of the web ACL\. 

## Setting the rule actions to count<a name="web-acl-rule-group-override-options-rules"></a>

You can override the actions of the rules inside a rule group, setting them to count for some or all of the rules\. If a rule's action is configured inside the rule group to something other than Count, this override changes that action so that matching requests are only counted\.  

When AWS WAF evaluates a web request against a rule with this count setting, if the request matches the rule, AWS WAF processes the match as a count and then continues evaluating the subsequent rules in the rule group\. The matching request generates count metrics, logs, and sampled requests\.

You can use this option to test a rule group before you implement it with its normal action settings\. If you apply this setting to all rules in a rule group, AWS WAF evaluates web requests against all of the rules and reports the matches that it finds in metrics, request samples, and logs\. At the end of the rule group evaluation, AWS WAF continues evaluating the rest of the rules that are in the web ACL\. 

You can also use this option to troubleshoot a rule group that's generating false positives\. False positives occur when a rule group blocks traffic that you aren't expecting it to block\. If you identify a rule within a rule group that would block requests that you want to allow through, you can keep this count action override on that rule, to exclude it from acting on your requests\.

For more information about using this in testing, see [Testing and tuning your AWS WAF protections](web-acl-testing.md)\.

For information about how to use this option, see [Setting rule actions to count in a rule group](web-acl-rule-group-settings.md#web-acl-rule-group-rule-to-count)\.

## Overriding the resulting rule group's action to count<a name="web-acl-rule-group-override-options-rule-group"></a>

You can override the action that the rule group returns, setting it to count\. 

**Note**  
This is not a good option for testing the rules in a rule group, because it doesn't alter how AWS WAF evaluates the rule group itself\. It only affects how AWS WAF handles results that are returned to the web ACL from the rule group evaluation\. If you want to test the rules in a rule group, use the option described in the preceding section, [Setting the rule actions to count](#web-acl-rule-group-override-options-rules)\.

When you override the rule group action to count, AWS WAF processes the rule group evaluation normally\. 

If no rules in the rule group match or if all matching rules have a count action, then this override has no effect on the processing of the rule group or the web ACL\.

The first rule in the rule group that matches a web request and that has a terminating rule action causes AWS WAF to stop evaluating the rule group and return the terminating action result to the web ACL evaluation level\. At this point, in the web ACL evaluation, this override takes effect\. AWS WAF overrides the terminating action so that the result of the rule group evaluation is only a count action\. AWS WAF then continues processing the rest of the rules in the web ACL\.

For information about how to use this option, see [Overriding a rule group's action to count](web-acl-rule-group-settings.md#web-acl-rule-group-action-override)\.