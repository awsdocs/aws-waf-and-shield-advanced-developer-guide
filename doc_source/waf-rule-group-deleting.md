# Deleting a rule group<a name="waf-rule-group-deleting"></a>

Follow the guidance in this section to delete a rule group\.

**Deleting referenced sets and rule groups**  
When you delete an entity that you can use in a web ACL, like an IP set, regex pattern set, or rule group, AWS WAF checks to see if the entity is currently being used in a web ACL\. If it finds that it is in use, AWS WAF warns you\. AWS WAF is almost always able to determine if an entity is being referenced by a web ACL\. However, in rare cases it might not be able to do so\. If you need to be sure that nothing is currently using the entity, check for it in your web ACLs before deleting it\. If the entity is a referenced set, also check that no rule groups are using it\.<a name="web-acl-deleting-procedure"></a>

**To delete a rule group**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Rule groups**\.

1. Choose the rule group that you want to delete, and then choose **Delete**\.