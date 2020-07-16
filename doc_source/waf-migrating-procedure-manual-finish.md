# Migrating a web ACL: manual follow\-up<a name="waf-migrating-procedure-manual-finish"></a>

After the automated migration is complete, review the newly created web ACL and fill in the components that the migration doesn't bring over for you\. The following procedure covers the aspects of web ACL management that the migration doesn't handle\. For the list, see [Migration caveats and limitations](waf-migrating-caveats.md)\.

**To finish the basic migration \- manual steps**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. The console should automatically use the latest version of AWS WAF\. To verify this, in the navigation pane, check that you can see the option **Switch to AWS WAF Classic**\. If you see **Switch to new AWS WAF**, choose that to switch to the latest version\. 

1. In the navigation pane, choose **Web ACLs**\. 

1. In the **Web ACLs** page, locate your new web ACL in the list for the Region where you created it\. Choose the web ACL's name to bring up the settings for the web ACL\. 

1. Review all of the settings for the new web ACL against your prior AWS WAF Classic web ACL\. By default, logging and protected resource associations are disabled\. You enable those when you're ready to switch over\. 

1. If your AWS WAF Classic web ACL had a rate\-based rule with a condition, the condition wasn't brought over in the migration\. You can add conditions to the rule in the new web ACL\. 

   1. In your web ACL settings page, choose the **Rules** tab\. 

   1. Locate your rate\-based rule in the list, select it, and choose **Edit**\.

   1. For **Criteria to count request towards rate limit**, select **Only consider requests that match the criteria in a rule statement**, then provide your additional criteria\. You can add the criteria using any rule statement that can be nested, including logical statements\. For information about your choices, see [Rule statements list](waf-rule-statements-list.md)\. 

1. If your AWS WAF Classic web ACL had a managed rule group, the rule group inclusion wasn't brought over in the migration\. You can add managed rule groups to the new web ACL\. Review the information about managed rule groups, including the list of free AWS Managed Rules that are available with the new version of AWS WAF, at [Managed rule groups](waf-managed-rule-groups.md)\. To add a managed rule group, do the following:

   1. In your web ACL settings page, choose the web ACL **Rules** tab\. 

   1. Choose **Add rules**, then choose **Add managed rule groups**\.

   1. Expand the listing for the vendor of your choice and select the rule groups that you want to add\. For AWS Marketplace sellers, you might need to subscribe to the rule groups\. For more information about using managed rule groups in your web ACL, see [Managed rule groups](waf-managed-rule-groups.md) and [How AWS WAF processes a web ACL](web-acl-processing.md)\.

After you finish the basic migration process, we recommend that you review your needs and consider additional options, to be sure that the new configuration is as efficient as possible and that it's using the latest available security options\. See [Migrating a web ACL: additional considerations](waf-migrating-procedure-additional.md)\.