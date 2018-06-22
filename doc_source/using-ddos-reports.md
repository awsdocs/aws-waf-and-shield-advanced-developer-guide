# Reviewing DDoS Incidents<a name="using-ddos-reports"></a>

AWS Shield Advanced provides real\-time metrics and reports for extensive visibility into attacks on your AWS resources\.

These metrics and reports are available only for AWS Shield Advanced customers\. To activate AWS Shield Advanced, see [To activate and AWS Shield Advanced](enable-ddos-prem.md#enable-ddos-prem-procedure)\.

You can view near real\-time metrics about attacks, including:
+ Attack type
+ Start time
+ Duration
+ Blocked packet per second
+ HTTP request samples

Details are available for active and past incidents that have occurred in the last 12 months\.

## Shield Advanced Details Report<a name="shield-details"></a>

Additionally, AWS Shield Advanced gives you insight into your overall traffic at the time of the attack\. You can review details about top:
+ IPs
+ URLs
+ Referrers
+ ASNs
+ Countries
+ User Agents

Use this information to create AWS WAF rules to help prevent future attacks\. For example, if you see that you have a lot of requests coming from a country that you don't typically do business in, you can create a AWS WAF rule to block requests from that country\.

**Note**  
You should always test your rules first by initially using `Count` rather than `Block`\. Once you are comfortable that the new rule is identifying the correct requests, you can modify your rule to block those requests\.<a name="review-ddos-reports-procedure"></a>

**To review DDoS incidents**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/waf/](https://console.aws.amazon.com/waf/)\. 

1. Choose **Incidents**\.

1. Choose the **Incident type** of the attack you want to investigate\.

If you determine a possible attack is underway, you can contact the DRT through the [AWS Support Center](https://console.aws.amazon.com/support/home#/), or attempt to mitigate the attack on your own by creating a new web access control list \(web ACL\)\. <a name="mitigating-ddos-attack-procedure"></a>

**To mitigate a potential DDoS attack**

1. Create conditions in AWS WAF that match the unusual behavior\.

1. Add those conditions to one or more AWS WAF rules\.

1. Add those rules to a web ACL and configure the web ACL to count the requests that match the rules\.

1. Monitor those counts to determine if the source of the requests should be blocked\. If the volume of requests continue to be unusually high, change your web ACL to block those requests\.

   For more information, see [Creating a Web ACL](web-acl-creating.md)\.

AWS provides preconfigured templates to get you started quickly\. The templates include a set of AWS WAF rules, which can be customized to best fit your needs, designed to block common web\-based attacks\. For more information, see [AWS WAF Security Automations](https://aws.amazon.com/answers/security/aws-waf-security-automations/)\.

## Monitoring Threats Across AWS<a name="aws-shield-global-threats"></a>

If you are a Shield Advanced customer, in addition to the information provided on the **Incidents** page about attacks on your own resources, you can use the global threat environment dashboard to view trends and metrics about the DDoS threat landscape across Amazon CloudFront, Elastic Load Balancing, and Route 53\.

The global threat environment dashboard provides a near real\-time summary of the global AWS threat landscape, including the largest attack, the top attack vectors, and the relative number of significant attacks\. You can customize the dashboard view for different time durations to see the history of significant DDoS attacks\.<a name="review-ddos-threat-dashboard"></a>

**To view the global threat environment dashboard**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/waf/](https://console.aws.amazon.com/waf/)\. 

1. Choose **Global threat environment**\.

1. Choose a time period\.

You can use the information on the global threat environment dashboard to better understand the threat landscape and help you make decisions to better protect your AWS resources\.