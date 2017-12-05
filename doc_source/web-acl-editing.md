# Editing a Web ACL<a name="web-acl-editing"></a>

To add or remove rules from a web ACL or change the default action, perform the following procedure\. 

**To edit a web ACL**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/waf/](https://console.aws.amazon.com/waf/)\. 

1. In the navigation pane, choose **Web ACLs**\.

1. Choose the web ACL that you want to edit\.

1. On the **Rules** tab in the right pane, choose **Edit web ACL**\.

1. To add rules to the web ACL, perform the following steps:

   1. In the **Rules** list, choose the rule that you want to add\. 

   1. Choose **Add rule to web ACL**\.

   1. Repeat steps a and b until you've added all the rules that you want\.

1. If you want to change the order of the rules in the web ACL, use the arrows in the **Order** column\. AWS WAF inspects web requests based on the order in which rules appear in the web ACL\. 

1. To remove a rule from the web ACL, choose the **x** at the right of the row for that rule\. This doesn't delete the rule from AWS WAF, it just removes the rule from this web ACL\.

1. To change the action for a rule or the default action for the web ACL, choose the preferred option\.
**Note**  
When setting the action for an AWS Marketplace rule group \(as opposed to a single rule\), the action you set for the rule group \(either **No override** or **Override to count**\) is called the override action\. For more information, see [Rule Group Override](waf-managed-rule-groups.md#waf-managed-rule-group-override)

1. Choose **Save changes**\.