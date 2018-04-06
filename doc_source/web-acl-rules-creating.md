# Creating a Rule and Adding Conditions<a name="web-acl-rules-creating"></a>

If you add more than one condition to a rule, a web request must match all the conditions for AWS WAF to allow or block requests based on that rule\.<a name="web-acl-rules-creating-procedure"></a>

**To create a rule and add conditions**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/waf/](https://console.aws.amazon.com/waf/)\. 

1. In the navigation pane, choose **Rules**\.

1. Choose **Create rule**\.

1. Type the following values:  
**Name**  
Type a name\.   
**CloudWatch metric name**  
Type a name for the CloudWatch metric that AWS WAF will create and will associate with the rule\. The name can contain only alphanumeric characters \(A\-Z, a\-z, 0\-9\) or the following special characters: \_\-\!"\#`\+\*\},\./\. It can't contain whitespace\.  
**Rule type**  
Choose either `Regular rule` or `Rate–based rule`\. Rate–based rules are identical to regular rules, but also take into account how many requests arrive from a specified IP address every five minutes\. For more information about these rule types, see [How AWS WAF Works](how-aws-waf-works.md)\.  
**Rate limit**  
If you are creating a rate–based rule, enter the maximum number of requests from a single IP address allowed in a five\-minute period\. The rate limit must be equal to or greater than 2000\.

1. To add a condition to the rule, specify the following values:   
**When a request does/does not**  
If you want AWS WAF to allow or block requests based on the filters in a condition, for example, web requests that originate from the range of IP addresses 192\.0\.2\.0/24, choose **does**\.  
If you want AWS WAF to allow or block requests based on the inverse of the filters in a condition, choose **does not**\. For example, if an IP match condition includes the IP address range 192\.0\.2\.0/24 and you want AWS WAF to allow or block requests that *do not* come from those IP addresses, choose **does not**\.  
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
   + If you add more than one condition, a web request must match at least one filter in every condition for AWS WAF to allow or block requests based on that rule 
   + If you add two IP match conditions to the same rule, AWS WAF will only allow or block requests that originate from IP addresses that appear in both IP match conditions 

1. When you're finished adding conditions, choose **Create**\.