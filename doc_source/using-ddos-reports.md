# Reviewing DDoS events<a name="using-ddos-reports"></a>

## Monitoring threats across AWS<a name="aws-shield-global-threats"></a>

Use the AWS Shield global threat dashboard to view trends and metrics about the DDoS threat landscape across Amazon EC2, Amazon CloudFront, Elastic Load Balancing, and Amazon Route 53\.

The global threat dashboard provides a near real\-time summary of the global AWS threat landscape, including the largest attack, the top attack vectors, and the relative number of significant attacks\. You can customize the dashboard view for different time durations to see the history of significant DDoS attacks\.

**Note**  
The console guidance provided here is for the latest version of the AWS Shield console, released in 2020\. In the console, you can switch between versions\. <a name="review-ddos-threat-dashboard"></a>

**To view the global threat dashboard**

1. Sign in to the AWS Management Console and open the AWS WAF & Shield console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the **AWS Shield** navigation bar, choose **Global threat dashboard**\.

1. Choose a time period\.

You can use the information on the global threat dashboard to better understand the threat landscape and help you make decisions to better protect your AWS resources\.

## Shield Advanced metrics and reports<a name="shield-details"></a>

AWS Shield Advanced provides real\-time metrics and reports for extensive visibility into events on your AWS resources\.

These metrics and reports are available only for AWS Shield Advanced customers\. To activate AWS Shield Advanced, see [To subscribe to AWS Shield Advanced](enable-ddos-prem.md#enable-ddos-prem-procedure)\.

You can view near real\-time metrics about events, including the following:
+ Attack type
+ Start time
+ Duration
+ Blocked packet per second
+ HTTP request samples

Details are available for active and past events that have occurred in the last 12 months\.

Additionally, AWS Shield Advanced gives you insight into your overall traffic at the time of the attack\. You can review details about the most prevalent:
+ IP addresses
+ URLs
+ Referrers
+ ASNs
+ Countries
+ User Agents

Use this information to create AWS WAF rules to help prevent future attacks\. For example, if you see that you have a lot of requests coming from a country that you don't typically do business in, you can create an AWS WAF rule to block requests from that country\. 

**Note**  
The console guidance provided here is for the latest version of the AWS Shield console, released in 2020\. In the console, you can switch between versions\. <a name="review-ddos-reports-procedure"></a>

**To review DDoS events**

1. Sign in to the AWS Management Console and open the AWS WAF & Shield console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the **AWS Shield** navigation bar, choose **Events**\.

The **Events** page provides the following possible current status for events:

**Mitigation in progress**  
Indicates a possible layer 3 or 4 attack has been identified and AWS is attempting to address the issue\.

**Mitigated**  
Indicates a possible layer 3 or 4 attack was identified\. AWS responded to the attack and the event appears to be over\.

**Identified \(ongoing\)**  
Indicates a possible layer 7 attack has been identified\. AWS cannot address layer 7 attacks, so you must design your own layer mitigation processes\. For more information on responding to possible layer 7 attacks, see [Responding to DDoS attacks](ddos-responding.md)\.

**Identified \(subsided\)**  
Indicates a possible layer 7 attack was identified and appears to be over\.

If you determine a possible attack is underway, you can contact the DDoS Response Team \(DRT\) through the [AWS Support Center](https://console.aws.amazon.com/support/home#/), or attempt to mitigate the attack on your own by creating a new web access control list \(web ACL\)\. <a name="mitigating-ddos-attack-procedure"></a>

**To mitigate a potential DDoS attack**

1. Create conditions in AWS WAF that match the unusual behavior\.

1. Add those conditions to one or more AWS WAF rules\.

1. Add those rules to a web ACL and configure the web ACL to count the requests that match the rules\.
**Note**  
You should always test your rules first by initially using `Count` rather than `Block`\. After you're comfortable that the new rule is identifying the correct requests, you can modify your rule to block those requests\.

1. Monitor those counts to determine if the source of the requests should be blocked\. If the volume of requests continues to be unusually high, change your web ACL to block those requests\.

   For more information, see [Creating a web ACL](web-acl-creating.md)\.

AWS provides preconfigured templates to get you started quickly\. The templates include a set of AWS WAF rules that you can customize and use to block common web\-based attacks\. For more information, see [AWS WAF Security Automations](https://aws.amazon.com/solutions/aws-waf-security-automations/)\.