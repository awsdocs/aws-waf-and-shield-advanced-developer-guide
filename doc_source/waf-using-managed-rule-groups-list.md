# Retrieving the list of managed rule groups<a name="waf-using-managed-rule-groups-list"></a>

The managed rule groups that are available for you to use in your web ACLs are the following: 
+ All AWS Managed Rules rule groups\.
+ The AWS Marketplace rule groups that you have subscribed to\. 
**Note**  
For information about subscribing to AWS Marketplace rule groups, see [AWS Marketplace managed rule groups](marketplace-managed-rule-groups.md)\.

When you retrieve the list of managed rule groups, the list you get back depends on the interface that you're using: 
+ **Console** – Through the console, you can see all managed rule groups, including the AWS Marketplace rule groups that you haven't subscribed to yet\. For the ones that you haven't subscribed to yet, the interface provides links that you can follow to subscribe\. 
+ **APIs and CLI** – Outside of the console, your request returns only the rule groups that are available for you to use\. 

**To retrieve the list of managed rule groups**
+ **Console** – During the process of creating a web ACL, on the **Add rules and rule groups** page, choose **Add managed rule groups**\. At the top level, the provider names are listed\. Expand each provider listing to see the list of managed rule groups\. For versioned rule groups, the information shown at this level is for the default version\. When you add a managed rule group to your web ACL, the console lists it based on the naming scheme `<Vendor Name>-<Managed Rule Group Name>`\. 
+ **API** –
  +  `ListAvailableManagedRuleGroups`
+ **CLI** –
  + `aws wafv2 list-available-managed-rule-groups --scope=<CLOUDFRONT|REGIONAL>`