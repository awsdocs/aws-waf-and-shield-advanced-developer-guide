# Adding and removing conditions in a rule<a name="classic-web-acl-rules-editing"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

You can change a rule by adding or removing conditions\. <a name="classic-web-acl-rules-editing-procedure"></a>

**To add or remove conditions in a rule**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Rules**\.

1. Choose the name of the rule in which you want to add or remove conditions\.

1. Choose **Add rule**\.

1. To add a condition, choose **Add condition** and specify the following values:  
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
   + Regular expression match conditions – choose **match at least one of the filters in the regex match condition**  
***condition name***  
Choose the condition that you want to add to the rule\. The list displays only conditions of the type that you chose in the preceding step\.

1. To remove a condition, select the **X** to the right of the condition name

1. Choose **Update**\.