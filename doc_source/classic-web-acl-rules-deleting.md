# Deleting a rule<a name="classic-web-acl-rules-deleting"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

If you want to delete a rule, you need to first remove the rule from the web ACLs that are using it and remove the conditions that are included in the rule\.<a name="classic-web-acl-rules-deleting-procedure"></a>

**To delete a rule**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. To remove the rule from the web ACLs that are using it, perform the following steps:

   1. In the navigation pane, choose **Web ACLs**\.

   1. Choose the name of a web ACL that is using the rule that you want to delete\.

   1. Choose **Edit web ACL**\.

   1. Choose the **X** to the right of the rule that you want to remove from the web ACL, and then choose **Update**\.

   1. Repeat for all of the remaining web ACLs that are using the rule that you want to delete\.

1. In the navigation pane, choose **Rules**\.

1. Select the name of the rule you want to delete\.

1. Choose **Delete**\.