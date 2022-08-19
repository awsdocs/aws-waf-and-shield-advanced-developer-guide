# Editing a web ACL<a name="web-acl-editing"></a>

To add or remove rules from a web ACL or change the default action, access the web ACL using the procedure on this page\. While updating a web ACL, AWS WAF provides continous coverage to the resources that you have associated with the web ACL\. 

**To edit a web ACL**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Web ACLs**\.

1. Choose the name of the web ACL that you want to edit\. The console takes you to the web ACL's description, where you can edit it\.
**Note**  
Web ACLs that are managed by AWS Firewall Manager have names that start with `FMManagedWebACLV2-`\. The Firewall Manager administrator manages these in Firewall Manager AWS WAF policies\. These web ACLs might contain rule group sets that are designated to run first and last in the web ACL, on either side of any rules or rule groups that you add and manage\. The first and last rule groups have names that start with `PREFMManaged-` and `POSTFMManaged-`, respectively\. For more information about these policies, see [AWS WAF policies](waf-policies.md)\.

1. Page through the web ACL definitions, and make your changes\. This is similar to the procedure that you use to create the web ACL in [Creating a web ACL](web-acl-creating.md), with the following exceptions\. 
   + Some fields that you set at creation aren't modifiable\. For example, you can't change the name of a web ACL, and for web ACLs that are managed by Firewall Manager, you can't change any first and last rule group specifications\. 
   + You can only set the CAPTCHA configuration for the web ACL when you edit an existing web ACL\. You can find this setting under the web ACL's **Rules** tab\. For information about using CAPTCHA, see [AWS WAF CAPTCHA](waf-captcha.md)\.

**Temporary inconsistencies during updates**  
When you create or change a web ACL or other AWS WAF resources, the changes take a small amount of time to propagate to all areas where the resources are stored\. The propagation time can be from a few seconds to a number of minutes\. 

The following are examples of the temporary inconsistencies that you might notice during change propagation: 
+ After you create a web ACL, if you try to associate it with a resource, you might get an exception indicating that the web ACL is unavailable\. 
+ After you add a rule group to a web ACL, the new rule group rules might be in effect in one area where the web ACL is used and not in another\.
+ After you change a rule action setting, you might see the old action in some places and the new action in others\. 
+ After you add an IP address to an IP set that is in use in a blocking rule, the new address might be blocked in one area while still allowed in another\.