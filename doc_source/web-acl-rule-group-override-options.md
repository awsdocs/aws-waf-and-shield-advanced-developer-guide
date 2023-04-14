# Action overrides in rule groups<a name="web-acl-rule-group-override-options"></a>

When you add a rule group to your web ACL, you can override the actions it takes on matching web requests\. Overriding the actions for a rule group inside your web ACL configuration doesn't alter the rule group itself\. It only alters how AWS WAF uses the rule group in the context of the web ACL\. 

## Rule action overrides<a name="web-acl-rule-group-override-options-rules"></a>

You can override the actions of the rules inside a rule group to any valid rule action\. When you do this, matching requests are handled exactly as if the configured rule's action were the override setting\. 

**Note**  
Rule actions can be terminating or non\-terminating\. A terminating action stops the web ACL evaluation of the request and either lets it continue to your protected application or blocks it\. 

Here are the rule action options: 
+ **Allow** – AWS WAF allows the request to be forwarded to the protected AWS resource for processing and response\. This is a terminating action\. In rules that you define, you can insert custom headers into the request before forwarding it to the protected resource\.
+ **Block** – AWS WAF blocks the request\. This is a terminating action\. By default, your protected AWS resource responds with an HTTP `403 (Forbidden)` status code\. In rules that you define, you can customize the response\. When AWS WAF blocks a request, the Block action settings determine the response that the protected resource sends back to the client\. 
+ **Count** – AWS WAF counts the request but does not determine whether to allow it or block it\. This is a non\-terminating action\. AWS WAF continues processing the remaining rules in the web ACL\. In rules that you define, you can insert custom headers into the request and you can add labels that other rules can match against\.
+ **CAPTCHA and Challenge** – AWS WAF uses CAPTCHA puzzles and silent challenges to verify that the request is not coming from a bot, and AWS WAF uses tokens to track recent successful client responses\. 
**Note**  
You are charged additional fees when you use the CAPTCHA or Challenge rule action in one of your rules or as a rule action override in a rule group\. For more information, see [AWS WAF Pricing](http://aws.amazon.com/waf/pricing/)\.

  These rule actions can be terminating or non\-terminating, depending on the state of the token in the request: 
  + **Non\-terminating for valid, unexpired token** – If the token is valid and unexpired according to the configured CAPTCHA or challenge immunity time, AWS WAF handles the request similar to the Count action\. AWS WAF continues to inspect the web request based on the remaining rules in the web ACL\. Similar to the Count configuration, in rules that you define, you can optionally configure these actions with custom headers to insert into the request, and you can add labels that other rules can match against\. 
  + **Terminating with blocked request for invalid or expired token** – If the token is invalid or the indicated timestamp is expired, AWS WAF terminates the inspection of the web request and blocks the request, similar to the Block action\. AWS WAF then responds to the client with an error\. For CAPTCHA, if the request contents indicate that the client browser can handle it, AWS WAF sends a CAPTCHA puzzle in a JavaScript interstitial, which is designed to distinguish human clients from bots\. For the Challenge action, AWS WAF sends a JavaScript interstitial with a silent challenge that is designed to distinguish normal browsers from sessions that are being run by bots\. 

  For additional information, see [CAPTCHA and Challenge actions in AWS WAF](waf-captcha-and-challenge.md)\.

For information about how to use this option, see [Overriding rule actions in a rule group](web-acl-rule-group-settings.md#web-acl-rule-group-rule-action-override)\.

**Overriding the rule action to Count**  
The most common use case for rule action overrides is overriding some or all of the rule actions to Count, to test and monitor a rule group's behavior before putting it into production\. 

You can also use this to troubleshoot a rule group that's generating false positives\. False positives occur when a rule group blocks traffic that you aren't expecting it to block\. If you identify a rule within a rule group that would block requests that you want to allow through, you can keep the count action override on that rule, to exclude it from acting on your requests\.

For more information about using the rule action override in testing, see [Testing and tuning your AWS WAF protections](web-acl-testing.md)\.

**JSON listing: `RuleActionOverrides` replaces `ExcludedRules`**  
If you set rule group rule actions to Count in your web ACL configuration before October 27, 2022, AWS WAF saved your overrides in the web ACL JSON as `ExcludedRules`\. Now, the JSON setting for overriding a rule to Count is in the `RuleActionOverrides` settings\. 

When you use the AWS WAF console to edit the existing rule group settings, the console automatically converts any `ExcludedRules` settings in the JSON to `RuleActionOverrides` settings, with the override action set to Count\. 
+ Current setting example: 

  ```
         "ManagedRuleGroupStatement": {
            "VendorName": "AWS",
            "Name": "AWSManagedRulesAdminProtectionRuleSet",
            "RuleActionOverrides": [
              {
                "Name": "AdminProtection_URIPATH",
                "ActionToUse": {
                  "Count": {}
                }
              }
            ]
  ```
+ Old setting example: 

  ```
  OLD SETTING
         "ManagedRuleGroupStatement": {
            "VendorName": "AWS",
            "Name": "AWSManagedRulesAdminProtectionRuleSet",
            "ExcludedRules": [
              {
                "Name": "AdminProtection_URIPATH"
              }
            ]
  OLD SETTING
  ```

We recommend that you update all of your `ExcludedRules` settings in your JSON listings to `RuleActionOverrides` settings with the action set to Count\. The API accepts either setting, but you'll get consistency in your JSON listings, between your console work and your API work, if you only use the new `RuleActionOverrides` setting\. 

## Rule group action override to Count<a name="web-acl-rule-group-override-options-rule-group"></a>

You can override the action that the rule group returns, setting it to Count\. 

**Note**  
This is not a good option for testing the rules in a rule group, because it doesn't alter how AWS WAF evaluates the rule group itself\. It only affects how AWS WAF handles results that are returned to the web ACL from the rule group evaluation\. If you want to test the rules in a rule group, use the option described in the preceding section, [Rule action overrides](#web-acl-rule-group-override-options-rules)\.

When you override the rule group action to Count, AWS WAF processes the rule group evaluation normally\. 

If no rules in the rule group match or if all matching rules have a Count action, then this override has no effect on the processing of the rule group or the web ACL\.

The first rule in the rule group that matches a web request and that has a terminating rule action causes AWS WAF to stop evaluating the rule group and return the terminating action result to the web ACL evaluation level\. At this point, in the web ACL evaluation, this override takes effect\. AWS WAF overrides the terminating action so that the result of the rule group evaluation is only a Count action\. AWS WAF then continues processing the rest of the rules in the web ACL\.

For information about how to use this option, see [Overriding a rule group's evaluation result to Count](web-acl-rule-group-settings.md#web-acl-rule-group-action-override)\.