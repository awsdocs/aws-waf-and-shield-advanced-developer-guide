# Step 3: Configure layer 7 DDoS mitigation<a name="ddos-get-started-rate-based-rules"></a>

We recommend that you add web ACLs with rate\-based rules as part of your AWS Shield Advanced protections\. These rules can alert you to sudden spikes in traffic that might indicate a potential DDoS event\. A rate\-based rule counts the requests that arrive from any individual address in any five\-minute period\. If the number of requests exceeds the limit that you define, the rule can trigger an action such as sending you a notification\. For more information about rate\-base rules, see [How AWS WAF works](how-aws-waf-works.md)\. 

**Note**  
If you used AWS Firewall Manager to create a Firewall Manager Shield Advanced policy, do not do this step\. Firewall Manager doesn't support rate\-based rules\.<a name="ddos-get-started-rate-based-rules-procedure"></a>

**To configure layer 7 DDoS mitigation for a Region**

Shield Advanced gives you the option to configure layer 7 DDoS mitigation for each Region where your chosen resources are located\. Perform the following procedure for each one\.

1. In the **Configure layer 7 DDoS mitigation** page, for each resource that isn't associated with a web ACL, either choose an existing web ACL or create a new web ACL\. 

   To create a web ACL, follow these steps:

   1. Choose **Create web ACL**\.

   1. Enter a name\. You can't change the name after you create the web ACL\.

   1. Choose **Create**\.
**Note**  
If a resource is already associated with a web ACL, you can't change to a different web ACL\. If you want to change the web ACL, you must first remove the associated web ACLs from the resource\. For more information, see [Associating or disassociating a Web ACL with an AWS resource](web-acl-associating-aws-resource.md)\.

1. For each associated web ACL that doesn't have a rate\-based rule defined, you can add one by choosing **Add rate limit rule** and then performing the following steps:

   1. Enter a name\.

   1. Enter a rate limit\. This is the maximum number of requests allowed in any five\-minute period from any single IP address before the rate\-based rule action is applied to the IP address\. When the requests from the IP address fall below the limit, the action is discontinued\. 

   1. Set the rule action to count or block requests from IP addresses while their request counts are over the limit\. The application and removal of the rule action might take effect a minute or two after the IP address request rate changes\. 

   1. Choose **Add rule**\.

1. Choose **Next**\.

**To continue without adding web ACLs or rate\-based rules**
+ Choose **Next**\.
**Important**  
If you use Shield Advanced within an AWS Firewall Manager Shield Advanced policy, you can't add a web ACL or rate\-based rule\. For all other resources, we recommend that, at a minimum, you attach a web ACL to each resource, even if that web ACL doesn't contain any rules\.

You can now go to [Step 4: Review and configure your settings](ddos-get-started-review-and-configure.md)\.