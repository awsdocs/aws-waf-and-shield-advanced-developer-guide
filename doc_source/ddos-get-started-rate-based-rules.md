# Step 3: Add web ACLs and rate\-based rules<a name="ddos-get-started-rate-based-rules"></a>

We recommend that you add web ACLs and rate\-based rules as part of your AWS Shield Advanced protections\. These rules can alert you to sudden spikes in traffic that might indicate a potential DDoS event\. A rate\-based rule counts the requests that arrive from any individual address in any five minute period\. If the number of requests exceeds the limit defined by you, the rule can trigger an action such as sending you a notification\. For more information about rate\-base rules, see [How AWS WAF works](how-aws-waf-works.md)\. 

**Note**  
If you have used AWS Firewall Manager to create a Firewall Manager\-Shield Advanced policy, do not do this step\. Firewall Manager doesn't support rate\-based rules\.<a name="ddos-get-started-rate-based-rules-procedure"></a>

**To add web ACLs or rate\-based rules**

1. In the **Add web ACLs and rules page**, for each resource that is listed in the table, either choose an existing web ACL or create a different web ACL\. To create a web ACL, follow these steps:

   1. From the **Associated web ACL** dropdown list, choose **Create a new web ACL**\.

   1. Enter a name\. You can't change the name after you create the web ACL\.

   1. Choose **Create web ACL**\.
**Note**  
If a resource is already associated with a web ACL, you can't change to a different web ACL\. If you want to change the web ACL, you must first remove the associated web ACLs from the resource\. For more information, see [Associating or disassociating a Web ACL with an AWS resource](web-acl-associating-aws-resource.md)\.

1. For each resource that is listed in the table that doesn't have a rate\-based rule defined, you can add one by selecting the action **Add one** and then performaing the following steps:

   1. Enter a name\.

   1. Enter a rate limit\. This is the maximum number of requests allowed in a five\-minute period from any single IP address\. 

   1. Set the rule action to count or block requests from IPs while their request counts are over the limit\.

   1. Choose **Create rule**\.

1. Choose **Apply web ACLs and rules**\.

**To continue without adding web ACLs or rate\-based rules**

1. Choose **Skip and go to next step**\.
**Important**  
We recommend that at a minimum you attach a web ACL to each resource, even if that web ACL doesn't contain any rules\.

1. For this tutorial, in the **Configure health based DDoS detection** page, choose **Skip and go to next step**\.

1. For this tutorial, in the **Create Amazon CloudWatch alarms and notifications** page, for any **SNS topic** dropdown, choose **No topic**\. Then choose **Create alarms**\.

You can now go to [Step 4: \(Optional\) Prepare for response team engagement](authorize-DRT.md)\.