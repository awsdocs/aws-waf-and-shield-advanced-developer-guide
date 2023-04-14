# Working with managed rule groups<a name="waf-using-managed-rule-groups"></a>

This section provides guidance for accessing and managing your managed rule groups\. 

When you add a managed rule group to your web ACL, you can choose the same configuration options as you can your own rule groups, plus additional settings\. 

Through the console, you access managed rule group information during the process of adding and editing the rules in your web ACLs\. Through the APIs and the command line interface \(CLI\), you can directly request managed rule group information\.

When you use a managed rule group in your web ACL, you can edit the following settings: 
+ **Version** – This is available only if the rule group is versioned\. For more information, see [Version management with managed rule groups](waf-managed-rule-groups-versioning.md)\.
+ **Override rule actions** – You can override the actions for rules in the rule group to any action\. Setting them to Count is useful for testing a rule group before using it to manage your web requests\. For more information, see [Rule action overrides](web-acl-rule-group-override-options.md#web-acl-rule-group-override-options-rules)\.
+ **Scope\-down statement** – You can add a scope\-down statement, to filter out web requests that you don't want to evaluate with the rule group\. For more information, see [Scope\-down statements](waf-rule-scope-down-statements.md)\.
+ **Override rule group action** – You can override the action that results from the rule group evaluation, and set it to Count only\. This option isn't commonly used\. It doesn't alter how AWS WAF evaluates the rules in the rule group\. For more information, see [Rule group action override to Count](web-acl-rule-group-override-options.md#web-acl-rule-group-override-options-rule-group)\.

**To edit the managed rule group settings in your web ACL**
+ **Console** 
  + \(Option\) When you add the managed rules group to your web ACL, you can choose **Edit** to view and edit the settings\. 
  + \(Option\) After you've added the managed rule group into your web ACL, from the **Web ACLs** page, choose the web ACL you just created\. This takes you to the web ACL edit page\. 
    + Choose **Rules**\. 
    + Select the rule group, then choose **Edit** to view and edit the settings\. 
+ **APIs and CLI** – Outside of the console, you can manage the managed rule group settings when you create and update the web ACL\. 