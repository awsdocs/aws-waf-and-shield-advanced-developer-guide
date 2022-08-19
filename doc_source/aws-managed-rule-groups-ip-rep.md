# IP reputation rule groups<a name="aws-managed-rule-groups-ip-rep"></a>

IP reputation rule groups allow you to block requests based on their source\. Choose one or more of these rule groups if you want to reduce your exposure to bot traffic or exploitation attempts, or if you are enforcing geographic restrictions on your content\. For bot management, see also [AWS WAF Bot Control rule group](aws-managed-rule-groups-bot.md)\.

The rule groups in this category don't provide versioning or SNS update notifications\. 

## Amazon IP reputation list managed rule group<a name="aws-managed-rule-groups-ip-rep-amazon"></a>

VendorName: `AWS`, Name: `AWSManagedRulesAmazonIpReputationList`, WCU: 25

The Amazon IP reputation list rule group contains rules that are based on Amazon internal threat intelligence\. This is useful if you would like to block IP addresses typically associated with bots or other threats\. Blocking these IP addresses can help mitigate bots and reduce the risk of a malicious actor discovering a vulnerable application\.


| Rule name | Description and label | 
| --- | --- | 
| AWSManagedIPReputationList |  Inspects for IP addresses that have been identified as bots by Amazon threat intelligence\.  Rule action: `Block` Label: `awswaf:managed:aws:amazon-ip-list:AWSManagedIPReputationList`  | 
| AWSManagedReconnaissanceList |  Inspects for connections from IP addresses that are performing reconnaissance against AWS resources\.  Rule action: `Block` Label: `awswaf:managed:aws:amazon-ip-list:AWSManagedReconnaissanceList`  | 

## Anonymous IP list managed rule group<a name="aws-managed-rule-groups-ip-rep-anonymous"></a>

VendorName: `AWS`, Name: `AWSManagedRulesAnonymousIpList`, WCU: 50

The Anonymous IP list rule group contains rules to block requests from services that allow the obfuscation of viewer identity\. These include requests from VPNs, proxies, Tor nodes, and hosting providers\. This rule group is useful if you want to filter out viewers that might be trying to hide their identity from your application\. Blocking the IP addresses of these services can help mitigate bots and evasion of geographic restrictions\.


| Rule name | Description and label | 
| --- | --- | 
| AnonymousIPList |  Inspects for a list of IP addresses of sources known to anonymize client information, like TOR nodes, temporary proxies, and other masking services\.  Rule action: `Block` Label: `awswaf:managed:aws:anonymous-ip-list:AnonymousIPList`  | 
| HostingProviderIPList | Inspects for a list of IP addresses from hosting and cloud providers, which are less likely to source end\-user traffic\. The IP list does not include AWS IP addresses\. Rule action: `Block` Label: `awswaf:managed:aws:anonymous-ip-list:HostingProviderIPList` | 