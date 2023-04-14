# Configure application layer \(layer 7\) DDoS protections with AWS WAF<a name="ddos-get-started-web-acl-rbr"></a>

To protect an application layer resource, Shield Advanced uses an AWS WAF web ACL with a rate\-based rule as a starting point\. AWS WAF is a web application firewall that lets you monitor the HTTP and HTTPS requests that are forwarded to your application layer resources, and lets you control access to your content based on the characteristics of the requests\. A rate\-based rule limits the volume of traffic from any single IP address, providing basic DDoS protection to your application\. For more information, see [How AWS WAF works](how-aws-waf-works.md) and [Rate\-based rule statement](waf-rule-statement-type-rate-based.md)\.

The base costs for using the AWS WAF web ACL with Shield Advanced is covered by your Shield Advanced subscription\. For pricing information and examples, see [AWS Shield Advanced Pricing](http://aws.amazon.com/shield/pricing/)\.

You can also optionally enable Shield Advanced automatic application layer DDoS mitigation, to have Shield Advanced automatically provide incident\-specific protections for you\. 

**Important**  
If you manage your Shield Advanced protections through AWS Firewall Manager using a Shield Advanced policy, you can't manage application layer protections here\. You must manage them in your Firewall Manager Shield Advanced policy\.

**To configure layer 7 DDoS protections for a Region**

Shield Advanced gives you the option to configure layer 7 DDoS mitigation for each Region where your chosen resources are located\. If you're adding protections in multiple regions, the wizard walks you through the following procedure for each Region\. 

1. The **Configure layer 7 DDoS protections** page lists each resource that isn't yet associated with a web ACL\. For each of these, either choose an existing web ACL or create a new web ACL\. For any resource that already has an associated web ACL, you can change web ACLs by first disassociating the current one through AWS WAF\. For more information, see [Associating or disassociating a web ACL with an AWS resource](web-acl-associating-aws-resource.md)\.

   For web ACLs that don't already have a rate\-based rule, the configuration wizard prompts you to add one\. A rate\-based rule limits traffic from IP addresses when they are sending a high volume of requests\. Rate\-based rules help protect your application against web request floods and can provide alerts about sudden spikes in traffic that might indicate a potential DDoS attack\. Add a rate\-based rule to a web ACL by choosing **Add rate limit rule** and then providing a rate limit and rule action\. You can configure additional protections in the web ACL through AWS WAF\. 

   For information about using web ACLs and rate\-based rules in your Shield Advanced protections, including additional configuration options for rate\-based rules, see [Shield Advanced application layer AWS WAF web ACLs and rate\-based rules](ddos-app-layer-web-ACL-and-rbr.md)\.

1. For **Automatic application layer DDoS mitigation**, if you want to have Shield Advanced automatically mitigate DDoS attacks against your application layer resources, choose **Enable** and then select the AWS WAF rule action that you want Shield Advanced to use in its custom rules\. This setting applies to all of the web ACLs for the resources that you are managing in this wizard session\. 

   With automatic application layer DDoS mitigation, Shield Advanced compares current traffic patterns against historic traffic baselines to detect deviations that might indicate a DDoS attack\. If automatic mitigation is enabled for a resource, when Shield Advanced detects a DDoS attack, it responds by creating, evaluating, and deploying custom AWS WAF rules to respond\. You specify whether the custom rules count or block attacks on your behalf\. 
**Note**  
Automatic application layer DDoS mitigation works only with web ACLs that were created using the latest version of AWS WAF \(v2\)\. 

   For more information about Shield Advanced automatic application layer DDoS mitigation, see [Shield Advanced automatic application layer DDoS mitigation](ddos-automatic-app-layer-response.md)\.

1. Choose **Next**\. The console wizard advances to the health\-based detection page\. 