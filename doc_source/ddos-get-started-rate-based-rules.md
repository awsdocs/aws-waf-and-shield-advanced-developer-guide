# Configure application layer \(layer 7\) DDoS protections<a name="ddos-get-started-rate-based-rules"></a>

For each application layer resource, Shield Advanced protection requires you to associate a web ACL with a rate\-based rule\. You can also optionally enable Shield Advanced automatic application layer DDoS mitigation\. 

**Important**  
If you manage your Shield Advanced protections through AWS Firewall Manager using a Shield Advanced policy, you can't manage the application layer protections here\. You must manage them in your Firewall Manager Shield Advanced policy\.

**To configure layer 7 DDoS protections for a Region**

Shield Advanced gives you the option to configure layer 7 DDoS mitigation for each Region where your chosen resources are located\. Perform the following procedure for each one\.
**Note**  
A resource can only be associated with one web ACL at a time\. If you want to change web ACLs for a resource, remove the current web ACL association, and then associate the new web ACL\. For more information, see [Associating or disassociating a web ACL with an AWS resource](web-acl-associating-aws-resource.md)\.

1. In the **Configure layer 7 DDoS protections** page, for each resource that isn't associated with a web ACL, either choose an existing web ACL or create a new web ACL\. 

   For any web ACL that doesn't have a rate\-based rule, the configuration wizard in Shield Advanced prompts you to create a new one\. Add a rate\-based rule to a web ACL by choosing **Add rate limit rule** and then providing a rate limit and rule action\. 

   For information about using web ACLs and rate\-based rules in your Shield Advanced protections, see [Shield Advanced application layer AWS WAF web ACLs and rate\-based rules](ddos-app-layer-web-ACL-and-rbr.md)\.

1. For **Automatic application layer DDoS mitigation**, if you want to have Shield Advanced automatically mitigate DDoS attacks against your application layer resources, choose **Enable** and then select the AWS WAF rule action that you want Shield Advanced to use in its custom rules\. This setting applies to all of the web ACLs for the resources that you are managing\. 

   With automatic application layer DDoS mitigation, Shield Advanced compares current traffic patterns against historic traffic baselines to detect deviations that might indicate a DDoS attack\. If automatic application layer DDoS mitigation is enabled for a resource, when Shield Advanced detects a DDoS attack, it responds by creating, evaluating, and deploying custom AWS WAF rules to respond to the attack\. You specify whether these custom rules count or block attacks on your behalf\. For more information about Shield Advanced automatic application layer DDoS mitigation, see [Shield Advanced automatic application layer DDoS mitigation](ddos-automatic-app-layer-response.md)\.
**Note**  
Automatic application layer DDoS mitigation works only with web ACLs that were created using the latest version of AWS WAF \(v2\)\. You cannot use automatic mitigation with AWS WAF Classic web ACLs\.

1. Choose **Next**\. The console wizard advances to the health\-based detection page\. 