# Step 3: Configure application layer \(layer 7\) DDoS protections<a name="ddos-get-started-rate-based-rules"></a>

You configure application layer protections by associating a web ACL to your resource, optionally enabling Shield Advanced automatic application layer DDoS mitigation, and adding a rate\-based rule to your web ACL\. 

**Important**  
If you manage your Shield Advanced protections through AWS Firewall Manager using a Shield Advanced policy, you can't manage the application layer protections here\. For all other resources, we recommend that, at a minimum, you attach a web ACL to each resource, even if the web ACL doesn't contain any rules\.<a name="ddos-get-started-rate-based-rules-procedure"></a>

**To configure layer 7 DDoS protections for a Region**

Shield Advanced gives you the option to configure layer 7 DDoS mitigation for each Region where your chosen resources are located\. Perform the following procedure for each one\.
**Note**  
A resource can only be associated with one web ACL at a time\. If you want to change web ACLs for a resource, remove the current web ACL association, and then associate the new web ACL\. For more information, see [Associating or disassociating a web ACL with an AWS resource](web-acl-associating-aws-resource.md)\.

1. In the **Configure layer 7 DDoS protections** page, for each resource that isn't associated with a web ACL, either choose an existing web ACL or create a new web ACL\. 

   To create a web ACL, follow these steps:

   1. Choose **Create web ACL**\.

   1. Enter a name\. You can't change the name after you create the web ACL\.

   1. Choose **Create**\.

1. For **Automatic application layer DDoS mitigation**, if you want to have Shield Advanced mitigate DDoS attacks against your Amazon CloudFront distributions, choose **Enable** and then select the AWS WAF rule action that you want Shield Advanced to use in its custom rules\. This setting applies to all of the web ACLs for the resources that you are managing\. 

   With automatic application layer DDoS mitigation, Shield Advanced compares current traffic patterns against historic traffic baselines to detect deviations that might indicate a DDoS attack\. If automatic application layer DDoS mitigation is enabled for a resource, when Shield Advanced detects a DDoS attack, it responds by creating, evaluating, and deploying custom AWS WAF rules to respond to the attack\. You specify whether these custom rules count or block attacks on your behalf\. For more information about Shield Advanced automatic application layer DDoS mitigation, see [Shield Advanced automatic application layer DDoS mitigation](ddos-advanced-automatic-app-layer-response.md)\.
**Note**  
Automatic application layer DDoS mitigation works with only web ACLs that were created using the latest version of AWS WAF \(v2\)\. You cannot use automatic mitigation with AWS WAF Classic web ACLs\.

1. For each web ACL that doesn't have a rate\-based rule defined, we recommend that you add one\. When you add a rate\-based rule to your web ACL, you can be alerted to sudden spikes in traffic that might indicate a potential DDoS attack\. A rate\-based rule counts the requests that arrive from any individual address in any 5\-minute period\. If the number of requests exceeds the limit that you define, the rule can trigger an action, such as sending you a notification\. For more information about rate\-base rules in AWS WAF, see [Rate\-based rule statement](waf-rule-statement-type-rate-based.md)\. 

   Add a rate\-based rule to a web ACL by choosing **Add rate limit rule** and then performing the following steps:

   1. Enter a name\.

   1. Enter a rate limit\. This is the maximum number of requests allowed in any 5\-minute period from any single IP address before the rate\-based rule action is applied to the IP address\. When the requests from the IP address fall below the limit, the action is discontinued\. 

   1. Set the rule action to count or block requests from IP addresses while their request counts are over the limit\. The application and removal of the rule action might take effect 1\-2 minutes after the IP address request rate changes\. 

   1. Choose **Add rule**\.

1. Choose **Next**\.

**To continue without adding web ACLs or rate\-based rules**
+ Choose **Next**\.

After you configure layer 7 protections, go to [Step 4: Review and configure your settings](ddos-get-started-review-and-configure.md)\.