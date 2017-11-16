# Deleting a Rule<a name="web-acl-rules-deleting"></a>

If you want to delete a rule, you need to first remove the rule from the web ACLs that are using it and remove the conditions that are included in the rule\.

**To delete a rule**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/waf/](https://console.aws.amazon.com/waf/)\. 

1. To remove the rule from the web ACLs that are using it, perform the following steps:

   1. In the navigation pane, choose **Web ACLs**\.

   1. Choose the name of a web ACL that is using the rule that you want to delete\.

   1. Choose **Edit web ACL**\.

   1. Choose the **X** to the right of the rule that you want to remove from the web ACL, and then choose **Update**\.

   1. Repeat for all of the remaining web ACLs that are using the rule that you want to delete\.

1. In the navigation pane, choose **Rules**\.

1. Select the name of the rule you want to delete\.

1. Choose **Delete**\.