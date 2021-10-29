# Retrieving the rules in a managed rule group<a name="waf-using-managed-rule-groups-rules"></a>

You can retrieve a list of the rules in a managed rule group\. The API and CLI calls return the rules specifications that you can reference in the JSON model or through AWS CloudFormation\.

**To retrieve the list of rules in a managed rule group**
+ **Console** 
  + \(Option\) When you add the managed rules group to your web ACL, you can choose **Edit** to view the rules\. 
  + \(Option\) After you've added the managed rule group into your web ACL, from the **Web ACLs** page, choose the web ACL you just created\. This takes you to the web ACL edit page\. 
    + Choose **Rules**\. 
    + Select the rule group you want to see a rules list for, then choose **Edit**\. AWS WAF shows the list of rules in the rule group\. 
+ **API** – `DescribeManagedRuleGroup`
+ **CLI** – `aws wafv2 describe-managed-rule-group --scope=<CLOUDFRONT|REGIONAL> --vendor-name <vendor> --name <managedrule_name>`