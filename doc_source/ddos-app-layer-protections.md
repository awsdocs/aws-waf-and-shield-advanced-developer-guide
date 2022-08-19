# AWS Shield Advanced application layer \(layer 7\) protections<a name="ddos-app-layer-protections"></a>

To protect your application layer resources with Shield Advanced, you start by associating an AWS WAF web ACL with the resource and adding one or more rate\-based rules to it\. You can additionally enable automatic application layer DDoS mitigation, which causes Shield Advanced to automatically create and manage web ACL rules on your behalf in response to DDoS attacks\. 

When you protect an application layer resource with Shield Advanced, Shield Advanced analyzes traffic over time to establish and maintain baselines\. Shield Advanced uses these baselines to detect anomalies in traffic patterns that might indicate a DDoS attack\. The point at which Shield Advanced detects an attack depends on the traffic that Shield Advanced has been able to observe prior to the attack and on the architecture you use for your web applications\. The architectural variations that can affect Shield Advanced behavior include the type of instance you use, your instance size, and whether the instance type supports enhanced networking\. You can also configure Shield Advanced to automatically place mitigations for application layer attacks\.

**Topics**
+ [Shield Advanced application layer AWS WAF web ACLs and rate\-based rules](ddos-app-layer-web-ACL-and-rbr.md)
+ [Shield Advanced automatic application layer DDoS mitigation](ddos-automatic-app-layer-response.md)