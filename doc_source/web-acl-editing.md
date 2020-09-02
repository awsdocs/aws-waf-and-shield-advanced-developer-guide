# Editing a Web ACL<a name="web-acl-editing"></a>

To add or remove rules from a web ACL or change the default action, access the web ACL using the following procedure:<a name="web-acl-editing-procedure"></a>

**To edit a web ACL**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Web ACLs**\.

1. Choose the name of the web ACL that you want to edit\. The console takes you to the web ACL's description, where you can edit it\.
**Note**  
Web ACLs that are managed by AWS Firewall Manager have names that start with `FMManagedWebACLV2`\. The Firewall Manager administrator manages these in Firewall Manager AWS WAF policies\. These web ACLs might contain rule group sets that are designated to run first and last in the web ACL, on either side of any rules or rule groups that you add and manage\. For more information about these policies, see [AWS WAF policies](waf-policies.md)\.

1. Page through the web ACL definitions, and make your changes\. This is the same as the procedure that you use to create the web ACL in [Creating a web ACL](web-acl-creating.md), but with some fields not modifiable\. For example, you can't change the name of a web ACL, and for web ACLs that are managed by Firewall Manager, you can't change any first and last rule group specifications\.