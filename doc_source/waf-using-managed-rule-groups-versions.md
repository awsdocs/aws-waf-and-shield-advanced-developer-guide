# Retrieving the available versions for a managed rule group<a name="waf-using-managed-rule-groups-versions"></a>

The available versions of a managed rule group are versions that haven't yet been scheduled to expire\. 

**To retrieve a list of the available versions of a managed rule group**
+ **Console** 
  + \(Option\) When you add the managed rule group to your web ACL, choose **Edit** to see the rule group's information\. Expand the **Version** dropdown to see the list of available versions\. 
  + \(Option\) After you've added the managed rule group into your web ACL, choose **Edit** on the web ACL, and then select and edit the rule group rule\. Expand the **Version** dropdown to see the list of available versions\. 
+ **API** –
  +  `ListAvailableManagedRuleGroupVersions`
+ **CLI** –
  +  `aws wafv2 list-available-managed-rule-group-versions --scope=<CLOUDFRONT|REGIONAL> --vendor-name <vendor> --name <managedrule_name>`