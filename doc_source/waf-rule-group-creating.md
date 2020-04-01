# Creating a rule group<a name="waf-rule-group-creating"></a>

**To create a rule group**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Rule groups**, and then **Create rule group**\. 

1. Enter a name and description for the rule group\. You'll use these to identify the set to manage it and use it\. 
**Note**  
You can't change the name after you create the rule group\.

1. For **Region**, choose the Region where you want to store the rule group\. To use a rule group in web ACLs that protect Amazon CloudFront distributions, you must use the global setting\. You can use the global setting for regional applications, too\.

1. Choose **Next**\.

1. Add rules to the rule group using the **Rule builder** wizard, the same as you do in web ACL management\. The only difference is that you can't add a rule group to another rule group\. 

1. For **Capacity**, set the maximum for the rule group's use of web ACL capacity units \(WCUs\)\. This is an immutable setting\. For information about WCUs, see [AWS WAF Web ACL capacity units \(WCU\)](how-aws-waf-works.md#aws-waf-capacity-units)\. 

   As you add rules to the rule group, the **Add rules and set capacity** pane displays the minimum required capacity, which is based on the rules that you've already added\. You can use this and your future plans for the rule group to help estimate the capacity that the rule group will require\. 

1. Review the settings for the rule group, and choose **Create**\.