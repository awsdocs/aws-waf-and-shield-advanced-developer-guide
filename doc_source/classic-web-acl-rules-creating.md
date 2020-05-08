# Creating a rule and adding conditions<a name="classic-web-acl-rules-creating"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

If you add more than one condition to a rule, a web request must match all the conditions for AWS WAF Classic to allow or block requests based on that rule\.<a name="classic-web-acl-rules-creating-procedure"></a>

**To create a rule and add conditions**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Rules**\.

1. Choose **Create rule**\.

1. Enter the following values:  
**Name**  
Enter a name\.   
**CloudWatch metric name**  
Enter a name for the CloudWatch metric that AWS WAF Classic will create and will associate with the rule\. The name can contain only alphanumeric characters \(A\-Z, a\-z, 0\-9\), with maximum length 128 and minimum length one\. It can't contain white space or metric names reserved for AWS WAF Classic, including "All" and "Default\_Action\.  
**Rule type**  
Choose either `Regular rule` or `Rate–based rule`\. Rate–based rules are identical to regular rules, but also take into account how many requests arrive from an IP address in a five\-minute period\. For more information about these rule types, see [How AWS WAF Classic works](classic-how-aws-waf-works.md)\.  
**Rate limit**  
For a rate\-based rule, enter the maximum number of requests to allow in any five\-minute period from an IP address that matches the rule's conditions\. The rate limit must be at least 100\.   
You can specify a rate limit alone, or a rate limit and conditions\. If you specify only a rate limit, AWS WAF places the limit on all IP addresses\. If you specify a rate limit and conditions, AWS WAF places the limit on IP addresses that match the conditions\.   
When an IP address reaches the rate limit threshold, AWS WAF applies the assigned action \(block or count\) as quickly as possible, usually within 30 seconds\. Once the action is in place, if five minutes pass with no requests from the IP address, AWS WAF resets the counter to zero\.

1. To add a condition to the rule, specify the following values:   
**When a request does/does not**  
If you want AWS WAF Classic to allow or block requests based on the filters in a condition, choose **does**\. For example, if an IP match condition includes the IP address range 192\.0\.2\.0/24 and you want AWS WAF Classic to allow or block requests that come from those IP addresses, choose **does**\.  
If you want AWS WAF Classic to allow or block requests based on the inverse of the filters in a condition, choose **does not**\. For example, if an IP match condition includes the IP address range 192\.0\.2\.0/24 and you want AWS WAF Classic to allow or block requests that *do not* come from those IP addresses, choose **does not**\.  
**match/originate from**  
Choose the type of condition that you want to add to the rule:  
   + Cross\-site scripting match conditions – choose **match at least one of the filters in the cross\-site scripting match condition**
   + IP match conditions – choose **originate from an IP address in**
   + Geo match conditions – choose **originate from a geographic location in**
   + Size constraint conditions – choose **match at least one of the filters in the size constraint condition**
   + SQL injection match conditions – choose **match at least one of the filters in the SQL injection match condition**
   + String match conditions – choose **match at least one of the filters in the string match condition**
   + Regular expression match conditions – choose **match at least one of the filters in the regex match condition**  
**condition name**  
Choose the condition that you want to add to the rule\. The list displays only conditions of the type that you chose in the preceding step\.

1. To add another condition to the rule, choose **Add another condition**, and repeat steps 4 and 5\. Note the following:
   + If you add more than one condition, a web request must match at least one filter in every condition for AWS WAF Classic to allow or block requests based on that rule 
   + If you add two IP match conditions to the same rule, AWS WAF Classic will only allow or block requests that originate from IP addresses that appear in both IP match conditions 

1. When you're finished adding conditions, choose **Create**\.