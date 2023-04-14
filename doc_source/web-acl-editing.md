# Editing a web ACL<a name="web-acl-editing"></a>

To add or remove rules from a web ACL or change configuration settings, access the web ACL using the procedure on this page\. While updating a web ACL, AWS WAF provides continuous coverage to the resources that you have associated with the web ACL\. 

**Production traffic risk**  
Before you deploy changes in your web ACL for production traffic, test and tune them in a staging or testing environment until you are comfortable with the potential impact to your traffic\. Then test and tune your updated rules in count mode with your production traffic before enabling them\. For guidance, see [Testing and tuning your AWS WAF protections](web-acl-testing.md)\.

**Note**  
Using more than 1,500 WCUs in a web ACL incurs costs beyond the basic web ACL price\. For more information, see [AWS WAF web ACL capacity units \(WCUs\)](aws-waf-capacity-units.md) and [AWS WAF Pricing](http://aws.amazon.com/waf/pricing/)\.

**To edit a web ACL**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Web ACLs**\.

1. Choose the name of the web ACL that you want to edit\. The console takes you to the web ACL's description\. 
**Note**  
Web ACLs that are managed by AWS Firewall Manager have names that start with `FMManagedWebACLV2-`\. The Firewall Manager administrator manages these in Firewall Manager AWS WAF policies\. These web ACLs might contain rule group sets that are designated to run first and last in the web ACL, on either side of any rules or rule groups that you add and manage\. You can't change any of these first and last rule group specifications\. The first and last rule groups have names that start with `PREFMManaged-` and `POSTFMManaged-`, respectively\. For more information about these policies, see [AWS WAF policies](waf-policies.md)\.

1. Edit the web ACL as needed\. Select the tabs for the configuration areas that you're interested in and edit the mutable settings\. For each setting that you edit, when you choose **Save** and return to the web ACL's description page, the console saves your changes to the web ACL\. 

   The following lists the tabs that contain web ACL configuration components\. 
   + **Rules** tab
     + **Rules defined in the web ACL** – The rules that you have defined in the web ACL\. You can edit and manage these in the same way as during web ACL creation\. For information about rules and rule group settings, see [Rules](waf-rules.md) and [Rule groups](waf-rule-groups.md)\.
     + **Web ACL rule capacity units used** – The current capacity usage for your web ACL\. This is view only\. 
     + **Default web ACL action for requests that don't match any rules**– For information about this setting, see [Deciding on the default action for a web ACL](web-acl-default-action.md)\. 
     + **Web ACL CAPTCHA and challenge configurations** – These immmunity times determine how long a CAPTCHA or challenge token remains valid after it's acquired\. You can only modify this setting here, after you create the web ACL\. For information about these settings, see [Timestamp expiration: token immunity times](waf-tokens-immunity-times.md)\.
     + **Token domain list** – AWS WAF accepts tokens for all domains in the list and for the domain of the associated resource\. For more information, see [Configuring the web ACL token domain list](waf-tokens-domains.md#waf-tokens-domain-lists)\.
   + **Associated AWS resources** tab
     + **Web request inspection size limit** – Included only for web ACLs that protect CloudFront distributions\. The body inspection size limit determines how much of the body component is forwarded to AWS WAF for inspection\. For more information about this setting, see [Body inspection size limits for CloudFront web ACLs](web-acl-setting-body-inspection-limit.md)\.
     + **Associated AWS resources** – The list of resources that the web ACL is currently associated with and protecting\. You can locate resources that are within the same Region as the web ACL and associate them to the web ACL\. For more information, see [Associating or disassociating a web ACL with an AWS resource](web-acl-associating-aws-resource.md)\.
   + **Custom response bodies** tab
     + Custom response bodies that are available for use by your web ACL rules that have the action set to Block\. For more information, see [Custom responses for Block actions](customizing-the-response-for-blocked-requests.md)\.
   + **Logging and metrics** tab
     + **Logging** – Logging for the traffic that the web ACL evaluates\. For information, see [Logging web ACL traffic](logging.md)\.
     + **Sampled requests** – Information about the rules that match web requests\. For information about viewing sampled requests, see [Viewing a sample of web requests](web-acl-testing-view-sample.md)\.
     + **CloudWatch metrics** – Metrics for the rules in your web ACL\. For information about Amazon CloudWatch metrics, see [Monitoring with Amazon CloudWatch](monitoring-cloudwatch.md)\. 

**Temporary inconsistencies during updates**  
When you create or change a web ACL or other AWS WAF resources, the changes take a small amount of time to propagate to all areas where the resources are stored\. The propagation time can be from a few seconds to a number of minutes\. 

The following are examples of the temporary inconsistencies that you might notice during change propagation: 
+ After you create a web ACL, if you try to associate it with a resource, you might get an exception indicating that the web ACL is unavailable\. 
+ After you add a rule group to a web ACL, the new rule group rules might be in effect in one area where the web ACL is used and not in another\.
+ After you change a rule action setting, you might see the old action in some places and the new action in others\. 
+ After you add an IP address to an IP set that is in use in a blocking rule, the new address might be blocked in one area while still allowed in another\.