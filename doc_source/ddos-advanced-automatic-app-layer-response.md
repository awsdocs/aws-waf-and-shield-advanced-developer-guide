# Shield Advanced automatic application layer DDoS mitigation<a name="ddos-advanced-automatic-app-layer-response"></a>

You can configure Shield Advanced to respond automatically to mitigate application layer \(layer 7\) attacks against your protected Amazon CloudFront distributions, by counting or blocking web requests that are part of the attack\. This option is an addition to the application layer protection that you add through Shield Advanced with an AWS WAF web ACL and rate\-based rule\. For information about the console steps, see [Configure application layer DDoS protections](manage-protection.md#add-rule-ddos)\.

Shield Advanced compares current traffic patterns against historic traffic baselines to detect deviations that might indicate a DDoS attack\. When you enable automatic application layer DDoS mitigation for a resource, Shield Advanced responds to detected DDoS attacks by creating, evaluating, and deploying custom AWS WAF rules to respond to the attack\. 

The following caveats apply to Shield Advanced automatic application layer DDoS mitigation:
+ Automatic application layer DDoS mitigation works with only Amazon CloudFront resources\. 
+ Automatic application layer DDoS mitigation works with only web ACLs that were created using the latest version of AWS WAF \(v2\)\. You cannot use automatic mitigation with AWS WAF Classic web ACLs\.
+ AWS Firewall Manager Shield Advanced policies do not currently support automatic application layer DDoS mitigation\. 
+ Automatic application layer DDoS mitigation does not interact with protection groups\. You can enable automatic mitigation for resources that are in protection groups, but Shield Advanced does not automatically apply attack mitigations based on protection group findings\. Shield Advanced applies automatic attack mitigations for individual resources\.

## Configuration required to enable automatic mitigation<a name="ddos-advanced-automatic-app-layer-response-config"></a>

You enable Shield Advanced automatic mitigation as part of the application layer DDoS protections for your resource\. For information about doing this through the console, see [Configure application layer DDoS protections](manage-protection.md#add-rule-ddos)\.

The automatic mitigation functionality requires you to do the following:
+ **Associate a web ACL with the resource** – This is required for any Shield Advanced application layer protection\. You can use the same web ACL for multiple resources\. We recommend doing this only for resources that have similar traffic\. For information about web ACLs, including the requirements for using them with multiple resources, see [How AWS WAF works](how-aws-waf-works.md)\.
+ **Enable and configure Shield Advanced automatic application layer DDoS mitigation** – When you enable this, you specify whether you want Shield Advanced to automatically block or count web requests that it determines to be part of a DDoS attack\. Shield Advanced adds a rule group to the associated web ACL and uses it to dynamically manage its response to DDoS attacks on the resource\. For information about the rule action settings, see [AWS WAF rule action](waf-rule-action.md)\.
+ **\(Optional, but recommended\) Add a rate\-based rule to the web ACL** – The rate\-based rule provides your resource with basic protection against DDoS attacks by preventing any individual IP address from sending too many requests in a short time\. For information about rate\-based rules, see [Rate\-based rule statement](waf-rule-statement-type-rate-based.md)\.

## What happens when you enable automatic mitigation<a name="ddos-advanced-automatic-app-layer-response-enable"></a>

Shield Advanced does the following when you enable automatic mitigation: 
+ **Adds a Shield Advanced rule group to the web ACL as needed** – If the web ACL that you have associated with the resource doesn't already have a Shield Advanced rule group reference statement, Shield Advanced adds one\. 
+ **Starts responding to DDoS attacks against the resource** – Shield Advanced automatically responds to DDoS attacks, as described in the sections that follow\. 

Shield Advanced uses a single rule group reference statement in any web ACL that you use for automatic mitigation\. If you're already using the web ACL for automatic mitigation, Shield Advanced doesn't add another rule group to it\. 

## The Shield Advanced rule group reference statement<a name="ddos-advanced-automatic-app-layer-response-rg"></a>

Shield Advanced creates its rule group reference statement in your web ACL with the following properties:
+ **Name** – `ShieldMitigationRuleGroup``_account-id_web-acl-id_unique-identifier`

  **Web ACL capacity units \(WCU\)** – 150\. These WCUs count against the WCU usage in your web ACL\. 

  **Priority** – 10,000,000\. This high priority setting allows you to run your other rules and rule groups in the web ACL before the Shield Advanced rule group\. AWS WAF runs the rules in a web ACL from the lowest numeric priority setting on up\. 

The automatic mitigation functionality doesn't consume any additional AWS WAF resources in your account, outside of the rule group WCUs in your web ACL\. For example, the Shield Advanced rule group isn't counted as one of your account's rule groups\. For information about account limits in AWS WAF, see [AWS WAF quotas](limits.md)\.

## How Shield Advanced responds to DDoS attacks with automatic mitigation<a name="ddos-advanced-automatic-app-layer-response-ddos-attack"></a>

When Shield Advanced detects an attack on a protected resource that has automatic mitigation enabled, it does the following:

1. Identifies the signatures of the web requests that make up the DDoS attack and creates rules to match against them\. In the rules, Shield Advanced applies the action setting that you've configured for the resource's automatic mitigation \- either `COUNT` or `BLOCK`\.

1. For all resources that are associated with the web ACL, Shield Advanced evaluates the new rules against recent historic traffic to ensure that they don't have unintended impact on normal historic traffic\. Shield Advanced runs these evaluations against the traffic for all resources that are associated with the web ACL\. 

1. If the rules are able to isolate only the traffic that's involved in the DDoS attack, Shield Advanced adds them to its managed rule group in the web ACL\. 

Throughout an attack, Shield Advanced sends the same notifications and provides the same event information as for basic Shield Advanced application layer protections\. You can see the information about events and DDoS attacks, and about any Shield Advanced mitigations for attacks, in the Shield Advanced event console\. For information, see [Reviewing DDoS events](using-ddos-reports.md)\. 

## What happens when you change the rule action setting<a name="ddos-advanced-automatic-app-layer-response-change-action"></a>

When you change the automatic mitigation rule action setting for a protected resource, Shield Advanced updates all rule settings for the resource\. It updates any rules that are currently in place for the resource in the managed rule group and it uses the new action setting when it creates new rules\. 

When you make changes to web ACLs or web ACL components, like rules and rule groups, AWS WAF propagates the changes everywhere that the web ACL and its components are stored and used\. Your changes are applied within seconds, but there might be a brief period of inconsistency when the changes have arrived in some places and not in others\. So, for example, if you change a rule action setting, the action might be the old action in one area and the new action in another area\. Or if you add an IP address to an IP set used in a blocking rule, the new address might briefly be blocked in one area while still allowed in another\. This temporary inconsistency can occur when you first associate a web ACL with an AWS resource and when you change a web ACL that is already associated with a resource\. Generally, any inconsistencies of this type last only a few seconds\.

You can change the rule action setting for your automatic mitigation configuration in the events page of the console, and through the application layer configuration page\. For information about the events page, see [Reviewing and responding to DDoS events](ddos-responding.md)\. For information about the configuration page, see [Configure application layer DDoS protections](manage-protection.md#add-rule-ddos)\.

## How Shield Advanced manages mitigations when an attack subsides<a name="ddos-advanced-automatic-app-layer-response-after-attack"></a>

When Shield Advanced determines that mitigating rules are not needed, it removes them from the Shield Advanced rule group\. 

The removal of mitigating rules won't necessarily coincide with the end of an attack\. Shield Advanced monitors patterns of attacks that it detects on your protected resources and proactively defends against recurrent attacks by keeping rules in place\. As needed, Shield Advanced increases the window of time that it keeps rules in place\. This way, Shield Advanced mitigates repeat attacks before they can impact your protected resources\.

## What happens when you disable automatic mitigation<a name="ddos-advanced-automatic-app-layer-response-disable"></a>

Shield Advanced does the following when you disable automatic mitigation for a resource: 
+ **Stops automatically responding to DDoS attacks** – Shield Advanced discontinues its automatic response activities for the resource\.
+ **Removes unneeded rules from the Shield Advanced rule group** – If Shield Advanced is maintaining any rules in its managed rule group on behalf of the protected resource, it removes them\. 
+ **Removes the Shield Advanced rule group, if it's no longer in use** – If the web ACL that you have associated with the resource isn't associated to any other resource that has automatic mitigation enabled, Shield Advanced removes its rule group reference statement from the web ACL\. 

## Best practices for using automatic mitigation<a name="ddos-advanced-automatic-app-layer-response-bp"></a>

Adhere to the guidance provided here when you use automatic mitigation\.
+ Don't delete any rule group from your web ACLs whose name starts with `ShieldMitigationRuleGroup`\. If you do, you disable the protections provided by Shield Advanced automatic mitigation for every resource that's associated with the web ACL\. Additionally, it can take Shield Advanced some time to receive notice of the change and to update its settings\. During this time, the Shield Advanced console pages will provide incorrect information\.
+ Manage all of your automatic mitigation protections through Shield Advanced\. 
+ Manage similar resources using the same web ACLs and protection settings, and manage dissimilar resources separately\. When Shield Advanced defines mitigating rules for DDoS attacks, it will only apply those rules if they don't negatively impact traffic on any of the resources that are associated with the web ACL\. 