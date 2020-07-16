# How AWS WAF processes a web ACL<a name="web-acl-processing"></a>

The way a web ACL handles a web request depends on the following: 
+ The action settings on the rules and web ACL
+ Any overrides that you place on the rules and rule groups that you add
+ The ordering of the rules and rule groups

If you add more than one rule to a web ACL, AWS WAF evaluates each request against the rules in the order that you list them in the web ACL\. If you add a rule group to your web ACL, AWS WAF processes the rule group in the order that it's listed in the web ACL and processes the rules in the rule group in the order that they're listed inside that\. 

## How AWS WAF handles the rule actions in a Web ACL<a name="web-acl-rule-actions"></a>

For the rules in a web ACL, you can choose between counting, allowing, or blocking matching web requests: 
+ Allow and block actions are terminating actions\. They stop all other processing of the web ACL on the matching web request\. If you include a rule in a web ACL that has an allow or block action and the rule finds a match, that match determines the final disposition of the web request for the web ACL\. AWS WAF doesn't process any other rules in the web ACL that come after the matching one\. This is true for rules that you add directly to the web ACL and rules that are inside an added rule group\. 
+ The count action is a non\-terminating action\. When a rule with a count action matches a request, AWS WAF counts the request, then continues processing the rules that follow in the web ACL rule set\. If the only rules that match have count action set, AWS WAF applies the web ACL default action setting\. 

The actions that AWS WAF applies to a web request are affected by the relative position of rules in the web ACL\. For example, if a web request matches a rule that allows requests and matches another rule that counts requests, if the rule that allows requests is listed first, then AWS WAF doesn't count the request\. 

## Deciding on the default action for a Web ACL<a name="web-acl-default-action"></a>

When you create and configure a web ACL, you set the web ACL default action, which determines how AWS WAF handles web requests that don't match any rules in the web ACL: 
+ **Allow** – If you want to allow most users to access your website, but you want to block access to attackers whose requests originate from specified IP addresses, or whose requests appear to contain malicious SQL code or specified values, choose allow for the default action\. Then, when you add rules to your web ACL, add rules that identify and block the specific requests that you want to block\.
+ **Block** – If you want to prevent most users from accessing your website, but you want to allow access to users whose requests originate from specified IP addresses, or whose requests contain specified values, choose block for the default action\. Then when you add rules to your web ACL, add rules that identify and allow the specific requests that you want to allow in\. 

Your configuration of your own rules and rule groups depends in part on whether you want to allow or block most web requests\. For example, if you want to *allow* most requests, you would set the web ACL default action to allow, and then add rules that identify web requests that you want to *block*, such as the following:
+ Requests that originate from IP addresses that are making an unreasonable number of requests
+ Requests that originate from countries that either you don't do business in or are the frequent source of attacks
+ Requests that include fake values in the `User-agent` header
+ Requests that appear to include malicious SQL code

Managed rule groups usually use the block action\. For information about managed rule groups, see [Managed rule groups](waf-managed-rule-groups.md)\.

## Overriding the actions of an entire rule group<a name="web-acl-override-actions"></a>

For each rule group in a web ACL, you can override the contained rule's actions, setting the action for all to count\. If any of the rule actions in the group is set to block or allow, this override changes the behavior so that matching rules are only counted\. In cases where the rule group might normally determine to allow or block a request, it doesn't, and the web ACL continues processing any rules that follow\. 

If you want to test a rule before you start using it to allow or block requests, you can configure AWS WAF to count the web requests that match the conditions in the rule\. If you have metrics enabled, you'll receive COUNT metrics for all the rules in the group\. For more information, see [Testing web ACLs](web-acl-testing.md)\.

## Excluding a rule in a rule group<a name="rule-group-rule-exclusion"></a>

For each rule group, you can exclude individual rules\. This effectively overrides the rule's action to count, so the effect on the rule is the same as the effect of **Override to count** for all rules in the group\. In cases where the rule might normally determine to allow or block a request, it doesn't, and the web ACL continues processing any rules that follow\.

Excluding a single rule can help you troubleshoot false positives, which is when a rule group blocks traffic that you aren't expecting it to block\. You can identify the rule within the rule group that's doing the unexpected blocking and then disable it by excluding it\. Excluding a rule overrides the action that's set on the rule to count\. If you have metrics enabled, you'll receive COUNT metrics for each excluded rule\.

## How AWS resources handle response delays from AWS WAF<a name="web-acl-processing-resource-default"></a>

On some occasions, AWS WAF might encounter an internal error that delays the response to associated AWS resources about whether to allow or block a request\. On those occasions, CloudFront typically allows the request or serves the content, while Amazon API Gateway and Application Load Balancer typically deny the request and don't serve the content\.