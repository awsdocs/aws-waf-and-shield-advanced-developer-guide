# AWS Managed Rules rule groups list<a name="aws-managed-rule-groups-list"></a>

This section describes the most recent versions of the AWS Managed Rules rule groups\. You see these on the console when you add a managed rule group to your web ACL\. Through the API, you can retrieve this list along with the AWS Marketplace managed rule groups that you're subscribed to by calling `ListAvailableManagedRuleGroups`\. 

**Note**  
For information about retrieving an AWS Managed Rules rule group's versions, see [Retrieving the available versions for a managed rule group](waf-using-managed-rule-groups-versions.md)\. 

All AWS Managed Rules rule groups support labeling, and the rule listings in this section include label specifications\. You can retrieve the labels for a managed rule group through the API by calling `DescribeManagedRuleGroup`\. The labels are listed in the `AvailableLabels` property in the response\. For information about labeling, see [Labels on web requests](waf-labels.md)\.

The information that we publish for the AWS Managed Rules rule group rules is intended to provide you with enough information to use the rules while not providing information that bad actors could use to circumvent the rules\. If you need more information than you find in this documentation, contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\. 

Test and tune any changes to your AWS WAF protections before you use them for production traffic\. For information, see [Testing and tuning your AWS WAF protections](web-acl-testing.md)\.

**Contents**
+ [Baseline rule groups](aws-managed-rule-groups-baseline.md)
  + [Core rule set \(CRS\) managed rule group](aws-managed-rule-groups-baseline.md#aws-managed-rule-groups-baseline-crs)
  + [Admin protection managed rule group](aws-managed-rule-groups-baseline.md#aws-managed-rule-groups-baseline-admin)
  + [Known bad inputs managed rule group](aws-managed-rule-groups-baseline.md#aws-managed-rule-groups-baseline-known-bad-inputs)
+ [Use\-case specific rule groups](aws-managed-rule-groups-use-case.md)
  + [SQL database managed rule group](aws-managed-rule-groups-use-case.md#aws-managed-rule-groups-use-case-sql-db)
  + [Linux operating system managed rule group](aws-managed-rule-groups-use-case.md#aws-managed-rule-groups-use-case-linux-os)
  + [POSIX operating system managed rule group](aws-managed-rule-groups-use-case.md#aws-managed-rule-groups-use-case-posix-os)
  + [Windows operating system managed rule group](aws-managed-rule-groups-use-case.md#aws-managed-rule-groups-use-case-windows-os)
  + [PHP application managed rule group](aws-managed-rule-groups-use-case.md#aws-managed-rule-groups-use-case-php-app)
  + [WordPress application managed rule group](aws-managed-rule-groups-use-case.md#aws-managed-rule-groups-use-case-wordpress-app)
+ [IP reputation rule groups](aws-managed-rule-groups-ip-rep.md)
  + [Amazon IP reputation list managed rule group](aws-managed-rule-groups-ip-rep.md#aws-managed-rule-groups-ip-rep-amazon)
  + [Anonymous IP list managed rule group](aws-managed-rule-groups-ip-rep.md#aws-managed-rule-groups-ip-rep-anonymous)
+ [AWS WAF Bot Control rule group](aws-managed-rule-groups-bot.md)
+ [AWS WAF Fraud Control account takeover prevention \(ATP\) rule group](aws-managed-rule-groups-atp.md)