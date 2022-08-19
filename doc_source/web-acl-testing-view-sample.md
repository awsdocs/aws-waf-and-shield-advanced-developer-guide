# Viewing a sample of web requests<a name="web-acl-testing-view-sample"></a>

In the AWS WAF console, if you have request sampling enabled, you can view a sample of the requests that AWS WAF has inspected and either allowed or blocked\. For each sampled request, you can view detailed data about the request, such as the originating IP address and the headers included in the request\. You can also view the rules that matched the request, and the rule action settings\.

The sample of requests contains up to 100 requests that matched the criteria for a rule in the web ACL and another 100 requests for requests that didn't match any rules and had the web ACL default action applied\. The requests in the sample come from all the protected resources that have received requests for your content in the previous three hours\. 

When a web request matches all the criteria in a rule and the action for that rule is **Count**, AWS WAF continues inspecting the web request using the subsequent rules in the web ACL\. Because of this, a web request could appear multiple times in the list of sampled requests\. 

**To view a sample of the web requests that a protected resource has forwarded to AWS WAF for inspection**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Web ACLs**\.

1. Choose the name of the web ACL for which you want to view requests\. The console takes you to the web ACL's description, where you can edit it\.

1. In the **Overview** tab, the **Sampled requests** table displays the following values for each request:  
**Metric name**  
The CloudWatch metric name for the rule in the web ACL that matched the request\. If a web request doesn't match any rule in the web ACL, this value is **Default**\.  
**Source IP**  
Either the IP address that the request originated from or, if the viewer used an HTTP proxy or an Application Load Balancer to send the request, the IP address of the proxy or Application Load Balancer\.   
**URI**  
The part of a URL that identifies a resource, for example, `/images/daily-ad.jpg`\.  
**Rule inside rule group**  
If the metric name identifies a rule group reference statement, this identifies the rule inside the rule group that matched the request\.   
**Action**  
Indicates whether the action for the corresponding rule is **Allow**, **Block**, or **Count**\.  
**Time**  
The time that AWS WAF received the request from the protected resource\. 

1. To display additional information about the components of the web request, choose the arrow on the left side of the row for that request\. 