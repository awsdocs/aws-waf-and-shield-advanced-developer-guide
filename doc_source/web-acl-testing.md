# Testing web ACLs<a name="web-acl-testing"></a>

To ensure that you don't accidentally configure AWS WAF to block web requests that you want to allow or allow requests that you want to block, we recommend that you test your web ACL thoroughly before you start using it on your website or web application\. 

**Topics**
+ [Counting the web requests that match the rules in a web ACL](#web-acl-testing-count)
+ [Viewing a sample of web requests](#web-acl-testing-view-sample)

## Counting the web requests that match the rules in a web ACL<a name="web-acl-testing-count"></a>

When you add rules to a web ACL, you specify whether you want AWS WAF to allow, block, or count the web requests that match all the conditions in that rule\. We recommend that you begin with the following configuration:
+ Configure all the rules in a web ACL to count web requests
+ Set the default action for the web ACL to allow requests

In this configuration, AWS WAF inspects each web request based on the conditions in the first rule\. If the web request matches all the conditions in that rule, AWS WAF increments a counter for that rule\. Then AWS WAF inspects the web request based on the conditions in the next rule\. If the request matches all the conditions in that rule, AWS WAF increments a counter for the rule\. This continues until AWS WAF has inspected the request based on the conditions in all of your rules\. 

After you've configured all the rules in a web ACL to count requests and associated the web ACL with one or more AWS resources \(Amazon API Gateway REST API, CloudFront distribution, or Application Load Balancer\) you can view the resulting counts in an Amazon CloudWatch graph\. For each rule in a web ACL and for all the requests that an associated resource forwards to AWS WAF for a web ACL, CloudWatch lets you do the following:
+ View data for the preceding hour or preceding three hours,
+ Change the interval between data points
+ Change the calculation that CloudWatch performs on the data, such as maximum, minimum, average, or sum

**Note**  
AWS WAF with CloudFront is a global service and metrics are available only when you choose the **US East \(N\. Virginia\)** Region in the AWS console\. If you choose another region, no AWS WAF metrics will appear in the CloudWatch console\.<a name="web-acl-testing-count-procedure"></a>

**To view data for the rules in a web ACL**

1. Sign in to the AWS Management Console and open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, under **Metrics**, choose **AWS/WAFV2**\.

1. Select the check box for the web ACL that you want to view data for\.

1. Change the applicable settings:  
**Statistic**  
Choose the calculation that CloudWatch performs on the data\.  
**Time range**  
Choose whether you want to view data for the preceding hour or the preceding three hours\.  
**Period**  
Choose the interval between data points in the graph\.  
**Rules**  
Choose the rules for which you want to view data\.

   Note the following:
   + If you recently associated a web ACL with an AWS resource, you might need to wait a few minutes for data to appear in the graph and for the metric for the web ACL to appear in the list of available metrics\.
   + If you associate more than one resource with a web ACL, the CloudWatch data will include requests for all of them\.
   + You can hover the mouse cursor over a data point to get more information\.
   + The graph doesn't refresh itself automatically\. To update the display, choose the refresh \(![\[Icon to refresh the CloudWatch graph\]](http://docs.aws.amazon.com/waf/latest/developerguide/images/cloudwatch-refresh-icon.png)\) icon\.

1. \(Optional\) View detailed information about individual requests that an associated AWS resource has forwarded to AWS WAF\. For more information, see [Viewing a sample of web requests](#web-acl-testing-view-sample)\.

1. If you determine that a rule is intercepting requests that you don't want it to intercept, change the applicable settings\. For more information, see [Managing and using a Web Access Control List \(Web ACL\)](web-acl.md)\.

   When you're satisfied that all of your rules are intercepting only the correct requests, change the action for each of your rules to **Allow** or **Block**\. For more information, see [Editing a Web ACL](web-acl-editing.md)\.

## Viewing a sample of web requests<a name="web-acl-testing-view-sample"></a>

In the AWS WAF console, if you have request sampling enabled, you can view a sample of the requests that an associated resource has forwarded to AWS WAF for inspection\. For each sampled request, you can view detailed data about the request, such as the originating IP address and the headers included in the request\. You also can view which rule the request matched, and whether the rule is configured to allow or block requests\.

The sample of requests contains up to 100 requests that matched all the conditions in each rule and another 100 requests for the default action, which applies to requests that didn't match all the conditions in any rule\. The requests in the sample come from all the API Gateway APIs, CloudFront edge locations or Application Load Balancers that have received requests for your content in the previous 15 minutes\.<a name="web-acl-testing-view-sample-procedure"></a>

**To view a sample of the web requests that an associated resource has forwarded to AWS WAF**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Web ACLs**

1. Choose the web ACL for which you want to view requests\.

1. In the **Overview** tab, the **Sampled requests** table displays the following values for each request:  
**Source IP**  
Either the IP address that the request originated from or, if the viewer used an HTTP proxy or an Application Load Balancer to send the request, the IP address of the proxy or Application Load Balancer\.   
**URI**  
The part of a URL that identifies a resource, for example, `/images/daily-ad.jpg`\.  
**Matches rule**  
Identifies the first rule in the web ACL for which the web request matched all the conditions\. If a web request doesn't match all the conditions in any rule in the web ACL, the value of **Matches rule** is **Default**\.  
Note that when a web request matches all the conditions in a rule and the action for that rule is **Count**, AWS WAF continues inspecting the web request based on subsequent rules in the web ACL\. In this case, a web request could appear twice in the list of sampled requests: once for the rule that has an action of **Count** and again for a subsequent rule or for the default action\.  
**Action**  
Indicates whether the action for the corresponding rule is **Allow**, **Block**, or **Count**\.  
**Time**  
The time that AWS WAF received the request from API Gateway, CloudFront or your Application Load Balancer\.

1. To display additional information about the request, choose the arrow on the left side of the IP address for that request\. AWS WAF displays the following information:  
**Source IP**  
The same IP address as the value in the **Source IP** column in the table\.  
**Country**  
The two\-letter country code of the country that the request originated from\. If the viewer used an HTTP proxy or an Application Load Balancer to send the request, this is the two\-letter country code of the country that the HTTP proxy or an Application Load Balancer is in\.  
For a list of two\-letter country codes and the corresponding country names, see the Wikipedia entry [ISO 3166\-1 alpha\-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2)\.  
**Method**  
The HTTP request method for the request: `GET`, `HEAD`, `OPTIONS`, `PUT`, `POST`, `PATCH`, or `DELETE`\.   
**URI**  
The same URI as the value in the **URI** column in the table\.  
**Request headers**  
The request headers and header values in the request\.

1. To refresh the list of sample requests, choose **Get new samples**\.