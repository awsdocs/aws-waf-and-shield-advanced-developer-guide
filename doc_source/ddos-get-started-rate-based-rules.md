# Step 3: Add Rate\-based Rules<a name="ddos-get-started-rate-based-rules"></a>

We recommend that you add rate\-based rules as part of your AWS Shield Advanced protections\. These rules can alert you to sudden spikes in traffic that might indicate a potential DDoS event\. A rate\-based rule counts the requests that arrive from a specified IP address every five minutes\. If the number of requests exceed a rate limit that you define, the rule can trigger an action such as sending you a notification\. For more information about rate\-base rules, see [How AWS WAF Works](how-aws-waf-works.md)\. 

**Important**  
If you have used AWS Firewall Manager to create a Firewall Manager\-Shield Advanced policy, do not do this step\. Firewall Manager does not support rate\-based rules\.<a name="ddos-get-started-rate-based-rules-procedure"></a>

**To add rate\-based rules**

1. For each resource that is listed in the table, choose an existing web ACL or alternatively create a different web ACL\. To create a web ACL, follow these steps:

   1. From the dropdown list, choose **New Web ACL**\.

   1. Enter a name\. You can't change the name after you create the web ACL\.

   1. Choose **Create web ACL**\.
**Note**  
If a resource is already associated with a web ACL, you can't change to a different web ACL\. If you want to change the ACL, you must first remove the associated web ACLs from the resource using the AWS WAF console\. For more information, see [Associating or Disassociating a Web ACL with an Amazon API Gateway API, a CloudFront Distribution or an Application Load Balancer](web-acl-associating-cloudfront-distribution.md)\.  
Only Amazon CloudFront distributions and Application Load Balancers will be listed in the table\. You can't associate web ACLs and rate\-based rules with other types of resources\.

1. For each resource that is listed in the table, choose an existing rate\-based rule\. Alternatively, you can create a different rate\-based rule by following these steps:

   1. From the dropdown list, choose **Create new rule**\. 

   1. Enter a name\.

   1. Enter a rate limit\. This is the maximum number of requests from a single IP address allowed in a five\-minute period\. The rate limit must be equal to or greater than 100\. 

   1. Choose the action to take if the rule is triggered\. **Block** will block the request\. **Count** will allow the request but increment a counter tracking how many times this rule was triggered\.

   1. Choose **Create rule**\.

   If you don't want to apply a rate\-based rule to a specific protection, you can choose **Do not apply rule** from the dropdown list\.

1. Choose **Continue**\.

**Important**  
You can continue from this step without adding any rate\-based rules or web ACLs\. However, we recommend that at a minimum you attach a web ACL to each resource, even if that web ACL doesn't contain any rules\.

You can now go to [Step 4: \(Optional\) Authorize the DDoS Response Team](authorize-DRT.md)\.