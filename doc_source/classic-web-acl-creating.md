# Creating a Web ACL<a name="classic-web-acl-creating"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. <a name="classic-web-acl-creating-procedure"></a>

**To create a web ACL**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. If this is your first time using AWS WAF Classic, choose **Go to AWS WAF Classic** and then **Configure Web ACL**\. If you've used AWS WAF Classic before, choose **Web ACLs** in the navigation pane, and then choose **Create web ACL**\.

1. For **Web ACL name**, enter a name\. 
**Note**  
You can't change the name after you create the web ACL\.

1. For **CloudWatch metric name**, change the default name if applicable\. The name can contain only alphanumeric characters \(A\-Z, a\-z, 0\-9\), with maximum length 128 and minimum length one\. It can't contain white space or metric names reserved for AWS WAF Classic, including "All" and "Default\_Action\."
**Note**  
You can't change the name after you create the web ACL\.

1. For **Region**, choose a Region\.

1.  For **AWS resource**, choose the resource that you want to associate with this web ACL, and then choose **Next**\.

1. If you've already created the conditions that you want AWS WAF Classic to use to inspect your web requests, choose **Next**, and then continue to the next step\.

   If you haven't already created conditions, do so now\. For more information, see the following topics:
   + [Working with cross\-site scripting match conditions](classic-web-acl-xss-conditions.md)
   + [Working with IP match conditions](classic-web-acl-ip-conditions.md)
   + [Working with geographic match conditions](classic-web-acl-geo-conditions.md)
   + [Working with size constraint conditions](classic-web-acl-size-conditions.md)
   + [Working with SQL injection match conditions](classic-web-acl-sql-conditions.md)
   + [Working with string match conditions](classic-web-acl-string-conditions.md)
   + [Working with regex match conditions](classic-web-acl-regex-conditions.md)

1. If you've already created the rules or rule groups \(or subscribed to an AWS Marketplace rule group\) that you want to add to this web ACL, add the rules to the web ACL:

   1. In the **Rules** list, choose a rule\.

   1. Choose **Add rule to web ACL**\.

   1. Repeat steps a and b until you've added all the rules that you want to add to this web ACL\.

   1. Go to step 10\.

1. If you haven't created rules yet, you can add rules now:

   1. Choose **Create rule**\.

   1. Enter the following values:  
**Name**  
Enter a name\.  
**CloudWatch metric name**  
Enter a name for the CloudWatch metric that AWS WAF Classic will create and will associate with the rule\. The name can contain only alphanumeric characters \(A\-Z, a\-z, 0\-9\), with maximum length 128 and minimum length one\. It can't contain white space or metric names reserved for AWS WAF Classic, including "All" and "Default\_Action\."  
You can't change the metric name after you create the rule\.

   1. To add a condition to the rule, specify the following values:   
**When a request does/does not**  
If you want AWS WAF Classic to allow or block requests based on the filters in a condition, for example, web requests that originate from the range of IP addresses 192\.0\.2\.0/24, choose **does**\.  
If you want AWS WAF Classic to allow or block requests based on the inverse of the filters in a condition, choose **does not**\. For example, if an IP match condition includes the IP address range 192\.0\.2\.0/24 and you want AWS WAF Classic to allow or block requests that *do not* come from those IP addresses, choose **does not**\.  
**match/originate from**  
Choose the type of condition that you want to add to the rule:  
      + Cross\-site scripting match conditions – choose **match at least one of the filters in the cross\-site scripting match condition**
      + IP match conditions – choose **originate from an IP address in**
      + Geo match conditions – choose **originate from a geographic location in**
      + Size constraint conditions – choose **match at least one of the filters in the size constraint condition**
      + SQL injection match conditions – choose **match at least one of the filters in the SQL injection match condition**
      + String match conditions – choose **match at least one of the filters in the string match condition**
      + Regex match conditions – choose **match at least one of the filters in the regex match condition**  
**condition name**  
Choose the condition that you want to add to the rule\. The list displays only conditions of the type that you chose in the preceding list\.

   1. To add another condition to the rule, choose **Add another condition**, and then repeat steps b and c\. Note the following:
      + If you add more than one condition, a web request must match at least one filter in every condition for AWS WAF Classic to allow or block requests based on that rule\. 
      + If you add two IP match conditions to the same rule, AWS WAF Classic will only allow or block requests that originate from IP addresses that appear in both IP match conditions\. 

   1. Repeat step 9 until you've created all the rules that you want to add to this web ACL\. 

   1. Choose **Create**\.

   1. Continue with step 10\.

1. For each rule or rule group in the web ACL, choose the kind of management you want AWS WAF Classic to provide, as follows: 
   + For each rule, choose whether you want AWS WAF Classic to allow, block, or count web requests based on the conditions in the rule:
     + **Allow** – API Gateway, CloudFront or an Application Load Balancer responds with the requested object\. In the case of CloudFront, if the object isn't in the edge cache, CloudFront forwards the request to the origin\.
     + **Block** – API Gateway, CloudFront or an Application Load Balancer responds to the request with an HTTP 403 \(Forbidden\) status code\. CloudFront also can respond with a custom error page\. For more information, see [Using AWS WAF Classic with CloudFront custom error pages](classic-cloudfront-features.md#classic-cloudfront-features-custom-error-pages)\.
     + **Count** – AWS WAF Classic increments a counter of requests that match the conditions in the rule, and then continues to inspect the web request based on the remaining rules in the web ACL\. 

       For information about using **Count** to test a web ACL before you start to use it to allow or block web requests, see [Counting the web requests that match the rules in a web ACL](classic-web-acl-testing.md#classic-web-acl-testing-count)\. 
   + For each rule group, set the override action for the rule group: 
     + **No override** – Causes the actions of the individual rules within the rule group to be used\.
     + **Override to count** – Overrides any block actions that are specifieid by individual rules in the group, so that all matching requests are only counted\. 

     For more information, see [Rule group override](classic-waf-managed-rule-groups.md#classic-waf-managed-rule-group-override)\.

1. If you want to change the order of the rules in the web ACL, use the arrows in the **Order** column\. AWS WAF Classic inspects web requests based on the order in which rules appear in the web ACL\. 

1. If you want to remove a rule that you added to the web ACL, choose the **x** in the row for the rule\.

1. Choose the default action for the web ACL\. This is the action that AWS WAF Classic takes when a web request doesn't match the conditions in any of the rules in this web ACL\. For more information, see [Deciding on the default action for a Web ACL](classic-web-acl-default-action.md)\.

1. Choose **Review and create**\.

1. Review the settings for the web ACL, and choose **Confirm and create**\.