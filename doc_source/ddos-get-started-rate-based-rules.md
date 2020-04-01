# Step 3: Add rate\-based rules<a name="ddos-get-started-rate-based-rules"></a>

We recommend that you add rate\-based rules as part of your AWS Shield Advanced protections\. These rules can alert you to sudden spikes in traffic that might indicate a potential DDoS event\. A rate\-based rule counts the requests that arrive from any individual address in any five minute period\. If the number of requests exceeds the limit defined by you, the rule can trigger an action such as sending you a notification\. For more information about rate\-base rules, see [How AWS WAF works](how-aws-waf-works.md)\. 

**Note**  
If you have used AWS Firewall Manager to create a Firewall Manager\-Shield Advanced policy, do not do this step\. Firewall Manager doesn't support rate\-based rules\.<a name="ddos-get-started-rate-based-rules-procedure"></a>

**To add rate\-based rules**

1. For each resource that is listed in the table, choose an existing web ACL or alternatively create a different web ACL\. To create a web ACL, follow these steps:

   1. From the dropdown list, choose **Create new web ACL**\.

   1. Enter a name\. You can't change the name after you create the web ACL\.

   1. Choose **Create web ACL**\.
**Note**  
If a resource is already associated with a web ACL, you can't change to a different web ACL\. If you want to change the web ACL, you must first remove the associated web ACLs from the resource\. For more information, see [Associating or disassociating a Web ACL with an AWS resource](web-acl-associating-aws-resource.md)\.  
The table shows the resources that you can associate with a web ACL\. These are Amazon CloudFront distributions, Amazon API Gateway APIs, and Application Load Balancers You can't associate web ACLs and rate\-based rules with other types of resources\.

1. For each resource that is listed in the table, in the **Rate\-based rule** dropdown, choose the rule setting that you want to apply\. If you want to apply a rate\-based rule, you can choose an existing rule or create a different rate\-based rule with the following steps:

   1. From the dropdown list, choose **Create new rule**\. 

   1. Enter a name\.

   1. Enter a rate limit\. This is the maximum number of requests allowed in a five\-minute period from any single IP address\. 

   1. Choose **Create rule**\.

   1. Optionally, on the resource line, use the **Action** dropdown list to modify the action to take if the rule is triggered\. **Block** will block the request\. **Count** will allow the request but increment a counter tracking how many times this rule was triggered\.

1. Choose **Apply web ACLs and rules**\.

**To continue without adding rate\-based rules**
+ Choose **Continue**\.
**Important**  
We recommend that at a minimum you attach a web ACL to each resource, even if that web ACL doesn't contain any rules\.

You can now go to [Step 4: \(Optional\) authorize the DDoS response team](authorize-DRT.md)\.