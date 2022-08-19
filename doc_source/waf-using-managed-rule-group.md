# Adding a managed rule group to a web ACL through the console<a name="waf-using-managed-rule-group"></a>

This guidance applies to all AWS Managed Rules rule groups and to the AWS Marketplace rule groups that you're subscribed to\. 

**Note**  
Test and tune all changes to your AWS WAF protections according to the guidance at [Testing and tuning your AWS WAF protections](web-acl-testing.md)\.

**To add a managed rule group to a web ACL through the console**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. Choose **Web ACLs** in the navigation pane\. 

1. In the **Web ACLs** page, from the list of web ACLs, select the one that you want to add the rule group to\. This takes you to the page for the single web ACL\.

1. In your web ACL's page, choose the **Rules** tab\. 

1. In the **Rules** pane, choose **Add rules**, then choose **Add managed rule groups**\. 

1. In the **Add managed rule groups** page, expand the selection for your rule group vendor, to see the list of available rule groups\. 

1. For each rule group that you want to add, choose **Add to web ACL**\. If you want to change the web ACL's configuration for the rule group, choose **Edit**, make your changes, and then choose **Save rule**\. For information about the options, see the versioning guidance at [Version management with managed rule groups](waf-managed-rule-groups-versioning.md) and the guidance for using a managed rule group in a web ACL at [Managed rule group statement](waf-rule-statement-type-managed-rule-group.md)\.

1. At the bottom of the **Add managed rule groups** page, choose **Add rules**\. 

1. In the **Set rule priority** page, adjust the order that the rules run as needed, then choose **Save**\. For more information, see [Processing order of rules and rule groups in a web ACL](web-acl-processing-order.md)\. 

In your web ACL's page, the managed rule groups that you've added are listed under the **Rules** tab\. 

Test and tune any changes to your AWS WAF protections before you use them for production traffic\. For information, see [Testing and tuning your AWS WAF protections](web-acl-testing.md)\.

**Temporary inconsistencies during updates**  
When you create or change a web ACL or other AWS WAF resources, the changes take a small amount of time to propagate to all areas where the resources are stored\. The propagation time can be from a few seconds to a number of minutes\. 

The following are examples of the temporary inconsistencies that you might notice during change propagation: 
+ After you create a web ACL, if you try to associate it with a resource, you might get an exception indicating that the web ACL is unavailable\. 
+ After you add a rule group to a web ACL, the new rule group rules might be in effect in one area where the web ACL is used and not in another\.
+ After you change a rule action setting, you might see the old action in some places and the new action in others\. 
+ After you add an IP address to an IP set that is in use in a blocking rule, the new address might be blocked in one area while still allowed in another\.