# Shield Advanced automatic application layer DDoS mitigation<a name="ddos-automatic-app-layer-response"></a>

You can configure Shield Advanced to respond automatically to mitigate application layer \(layer 7\) attacks against your protected application layer resources, by counting or blocking web requests that are part of the attack\. This option is an addition to the application layer protection that you add through Shield Advanced with an AWS WAF web ACL and rate\-based rule\. For information about the console steps, see [Configure application layer DDoS protections](ddos-manage-protected-resources.md#configure-app-layer-protection)\.

Shield Advanced compares current traffic patterns against historic traffic baselines to detect deviations that might indicate a DDoS attack\. When you enable automatic application layer DDoS mitigation for a resource, Shield Advanced responds to detected DDoS attacks by creating, evaluating, and deploying custom AWS WAF rules\. 

## Shield Advanced automatic application layer DDoS mitigation caveats<a name="ddos-automatic-app-layer-response-caveats"></a>

The following list describes the caveats of Shield Advanced automatic application layer DDoS mitigation, and describes steps that you might want to take in response\.
+ Automatic application layer DDoS mitigation works only with web ACLs that were created using the latest version of AWS WAF \(v2\)\. You cannot use automatic mitigation with AWS WAF Classic web ACLs\.
+ For detection and automatic mitigation of application layer attacks, Shield Advanced leverages the historical traffic to your protected resource\. Awareness of the normal traffic patterns to your application is what enables Shield Advanced to isolate attack traffic from the normal traffic to your application\. If your protected resource doesn’t yet have a history of normal application traffic \(e\.g\. before an application is launched\) or lacks production traffic for extended periods of time, we recommend enabling the automatic mitigation in `COUNT` mode until a history of normal application traffic has been established for the resource\.
+ Automatic application layer DDoS mitigation only places rules to mitigate a DDoS attack after testing them against historical traffic to verify that they mitigate the attack traffic and don't impact the normal traffic to your application\.
+ The time between the start of a DDoS attack and when Shield Advanced places automatic mitigation rules varies with each event\. Some DDoS attacks might end before mitigation rules are deployed\. Other attacks might happen when a mitigation is already in place, and so might be mitigated from the start of the event\.
+ For Application Load Balancers that receive any traffic through a content delivery network \(CDN\), such as Amazon CloudFront, the application\-layer automatic mitigation capabilities of Shield Advanced for those Application Load Balancer resources will be reduced\. Shield Advanced uses client traffic attributes to identify and isolate attack traffic from normal traffic to your application, and CDNs may not preserve or forward the original client traffic attributes\. If you use CloudFront, we recommend enabling automatic mitigation on the CloudFront distribution\.
+ Automatic application layer DDoS mitigation does not interact with protection groups\. You can enable automatic mitigation for resources that are in protection groups, but Shield Advanced does not automatically apply attack mitigations based on protection group findings\. Shield Advanced applies automatic attack mitigations for individual resources\.

**Contents**
+ [Shield Advanced automatic application layer DDoS mitigation caveats](#ddos-automatic-app-layer-response-caveats)
+ [Best practices for using automatic mitigation](ddos-automatic-app-layer-response-bp.md)
+ [Configuration required to enable automatic mitigation](ddos-automatic-app-layer-response-config.md)
+ [How Shield Advanced manages automatic mitigation](ddos-automatic-app-layer-response-behavior.md)
  + [What happens when you enable automatic mitigation](ddos-automatic-app-layer-response-behavior.md#ddos-automatic-app-layer-response-enable)
  + [How Shield Advanced responds to DDoS attacks with automatic mitigation](ddos-automatic-app-layer-response-behavior.md#ddos-automatic-app-layer-response-ddos-attack)
  + [What happens when you change the rule action setting](ddos-automatic-app-layer-response-behavior.md#ddos-automatic-app-layer-response-change-action)
  + [How Shield Advanced manages mitigations when an attack subsides](ddos-automatic-app-layer-response-behavior.md#ddos-automatic-app-layer-response-after-attack)
  + [What happens when you disable automatic mitigation](ddos-automatic-app-layer-response-behavior.md#ddos-automatic-app-layer-response-disable)
+ [The Shield Advanced rule group reference statement](ddos-automatic-app-layer-response-rg.md)
+ [Managing automatic application layer DDoS mitigation](manage-automatic-app-layer-response.md)
  + [Enabling and disabling automatic application layer DDoS mitigation](manage-automatic-app-layer-response.md#enable-disable-automatic-app-layer-response)
  + [Changing the action used for automatic application layer DDoS mitigation](manage-automatic-app-layer-response.md#change-action-of-automatic-app-layer-response)