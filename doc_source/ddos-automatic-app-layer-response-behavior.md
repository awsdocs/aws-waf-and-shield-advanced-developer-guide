# How Shield Advanced manages automatic mitigation<a name="ddos-automatic-app-layer-response-behavior"></a>

The topics in section describe how Shield Advanced handles your configuration changes for automatic application layer DDoS mitigation and how it handles DDoS attacks when automatic mitigation is enabled\. 

**Topics**
+ [What happens when you enable automatic mitigation](#ddos-automatic-app-layer-response-enable)
+ [How Shield Advanced responds to DDoS attacks with automatic mitigation](#ddos-automatic-app-layer-response-ddos-attack)
+ [What happens when you change the rule action setting](#ddos-automatic-app-layer-response-change-action)
+ [How Shield Advanced manages mitigations when an attack subsides](#ddos-automatic-app-layer-response-after-attack)
+ [What happens when you disable automatic mitigation](#ddos-automatic-app-layer-response-disable)

## What happens when you enable automatic mitigation<a name="ddos-automatic-app-layer-response-enable"></a>

Shield Advanced does the following when you enable automatic mitigation: 
+ **As needed, adds a rule group for Shield Advanced use** – If the AWS WAF web ACL that you have associated with the resource doesn't already have an AWS WAF rule group reference statement that's dedicated to automatic application layer DDoS mitigation, Shield Advanced adds one\. The name of the rule group reference statement starts with `ShieldMitigationRuleGroup`\. For additional details about this rule group, see [The Shield Advanced rule group reference statement](ddos-automatic-app-layer-response-rg.md)\.
+ **Starts responding to DDoS attacks against the resource** – Shield Advanced automatically responds to DDoS attacks for the protected resource\. Shield Advanced uses the rule group to deploy AWS WAF rules for DDoS attack mitigation\. Shield Advanced tailors these rules to your application and to the attacks that your application experiences, and tests them against the resource's historical traffic before deploying them\. The sections that follow provide more information about how Shield Advanced does this\.

Shield Advanced uses a single rule group reference statement in any web ACL that you use for automatic mitigation\. If you're already using the web ACL for automatic mitigation, Shield Advanced doesn't add another rule group to it\. Automatic application layer DDoS mitigation depends on the presence of the rule group to mitigate attacks\. If the rule group is removed from the AWS WAF web ACL for any reason, the removal disables automatic mitigation for all resources that are associated with the web ACL\.

## How Shield Advanced responds to DDoS attacks with automatic mitigation<a name="ddos-automatic-app-layer-response-ddos-attack"></a>

When Shield Advanced detects an attack on a protected resource that has automatic mitigation enabled, it does the following:

1. Attempts to identify an attack signature that isolates the attack traffic from the normal traffic to your application\. The goal is to produce high quality DDoS mitigation rules that, when placed, affect only the attack traffic and don't impact normal traffic to your application\.

1. Evaluates the identified attack signature against the historical traffic patterns for the resource that's under attack as well as for any other resource that's associated with the same web ACL\. Shield Advanced does this before it deploys any rules in response to the event\. 

   Depending on the evaluation results, Shield Advanced does one of the following: 
   + If Shield Advanced determines that the attack signature isolates only the traffic that is involved in the DDoS attack, it implements the signature in AWS WAF rules under the Shield Advanced mitigation rule group in the web ACL\. Shield Advanced gives these rules the action setting that you've configured for the resource's automatic mitigation \- either `COUNT` or `BLOCK`\.
   + Otherwise, Shield Advanced doesn't place a mitigation\.

Throughout an attack, Shield Advanced sends the same notifications and provides the same event information as for basic Shield Advanced application layer protections\. You can see the information about events and DDoS attacks, and about any Shield Advanced mitigations for attacks, in the Shield Advanced event console\. For information, see [Visibility into DDoS events](ddos-viewing-events.md)\. 

If you've configured automatic mitigation to use the `BLOCK` rule action and you experience false positives from the mitigation rules that Shield Advanced has deployed, you can change the rule action to `COUNT`\. For information about how to to this, see [Changing the action used for automatic application layer DDoS mitigation](manage-automatic-app-layer-response.md#change-action-of-automatic-app-layer-response)\. 

## What happens when you change the rule action setting<a name="ddos-automatic-app-layer-response-change-action"></a>

When you change the automatic mitigation rule action setting for a protected resource, Shield Advanced updates all rule settings for the resource\. It updates any rules that are currently in place for the resource in the managed rule group and it uses the new action setting when it creates new rules\. 

Changing the action setting can take a few seconds to propagate\. During this time, you might see the old setting in some places where the rule group is in use, and the new setting in other places\. 

You can change the rule action setting for your automatic mitigation configuration in the events page of the console, and through the application layer configuration page\. For information about the events page, see [Responding to DDoS events](ddos-responding.md)\. For information about the configuration page, see [Configure application layer DDoS protections](ddos-manage-protected-resources.md#configure-app-layer-protection)\.

## How Shield Advanced manages mitigations when an attack subsides<a name="ddos-automatic-app-layer-response-after-attack"></a>

When Shield Advanced determines that mitigation rules that were deployed for a particular attack are no longer needed, it removes them from the Shield Advanced mitigation rule group\. 

The removal of mitigating rules won't necessarily coincide with the end of an attack\. Shield Advanced monitors patterns of attack that it detects on your protected resources\. It might proactively defend against the recurrence of an attack with a specific signature by keeping the rules that it has deployed against the initial occurrence of that attack in place\. As needed, Shield Advanced increases the window of time that it keeps rules in place\. This way, Shield Advanced might mitigate repeated attacks with a specific signature before they impact your protected resources\. 

## What happens when you disable automatic mitigation<a name="ddos-automatic-app-layer-response-disable"></a>

Shield Advanced does the following when you disable automatic mitigation for a resource: 
+ **Stops automatically responding to DDoS attacks** – Shield Advanced discontinues its automatic response activities for the resource\.
+ **Removes unneeded rules from the Shield Advanced rule group** – If Shield Advanced is maintaining any rules in its managed rule group on behalf of the protected resource, it removes them\. 
+ **Removes the Shield Advanced rule group, if it's no longer in use** – If the web ACL that you have associated with the resource isn't associated to any other resource that has automatic mitigation enabled, Shield Advanced removes its rule group reference statement from the web ACL\. 