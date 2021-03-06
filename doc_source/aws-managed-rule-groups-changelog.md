# AWS Managed Rules changelog<a name="aws-managed-rule-groups-changelog"></a>

This section lists changes to the AWS Managed Rules for AWS WAF since their release in November, 2019\.

**Note**  
This changelog reports changes to the rules and rule groups in AWS Managed Rules for AWS WAF\. It doesn't report changes to the IP address lists that are used by the rules in the [IP reputation rule groups](aws-managed-rule-groups-list.md#aws-managed-rule-groups-ip-rep), due to the dynamic nature of those lists\.


| Rule group | Rules affected | Description | Date | 
| --- | --- | --- | --- | 
| Amazon IP reputation list | `AWSManagedIPReputationList_xxxx` | Restructured the IP reputation list, removed suffixes from rule name, and added support for AWS WAF labels\.  | 2021\-05\-04 | 
| Anonymous IP list | `AnonymousIPList` `HostingProviderList` | Added support for AWS WAF labels\.  | 2021\-05\-04 | 
| AWS WAF Bot Control | All | Added the Bot Control rule set\.  | 2021\-04\-01 | 
| Core rule set \(CRS\) | `GenericRFI_QUERYARGUMENTS`  | Added double URL decode\.  | 2021\-03\-03 | 
| Core rule set \(CRS\) | `RestrictedExtensions_URIPATH`  | Improved the configuration of the rules and added an extra URL decode\.  | 2021\-03\-03 | 
| Admin protection | `AdminProtection_URIPATH`  | Added double URL decode\.  | 2021\-03\-03 | 
| Known bad inputs | `ExploitablePaths_URIPATH`  | Improved the configuration of the rules and added an extra URL decode\.  | 2021\-03\-03 | 
| Linux operating system | `LFI_QUERYARGUMENTS`  | Improved the configuration of the rules and added an extra URL decode\.  | 2021\-03\-03 | 
| Windows operating system | All | Improved the configuration of the rules\.  | 2020\-09\-23 | 
| PHP application | `PHPHighRiskMethodsVariables_QUERYARGUMENTS` `PHPHighRiskMethodsVariables_BODY`  | Changed the text transformation from HTML decode to URL decode, to improve blocking\.  | 2020\-09\-16 | 
| POSIX operating system | `UNIXShellCommandsVariables_QUERYARGUMENTS` `UNIXShellCommandsVariables_BODY`  | Changed the text transformation from HTML decode to URL decode, to improve blocking\.  | 2020\-09\-16 | 
| Core rule set | `GenericLFI_QUERYARGUMENTS` `GenericLFI_URIPATH` GenericLFI\_BODY  | Changed the text transformation from HTML decode to URL decode, to improve blocking\.  | 2020\-08\-07 | 
| Linux operating system | `LFI_URIPATH` `LFI_QUERYARGUMENTS` `LFI_BODY`  | Changed the text transformation from HTML entity decode to URL decode, to improve detection and blocking\.  | 2020\-05\-19 | 
| Anonymous IP List | All | New rule group in [IP reputation rule groups](aws-managed-rule-groups-list.md#aws-managed-rule-groups-ip-rep) to block requests from services that allow the obfuscation of viewer identity, to help mitigate bots and evasion of geographic restrictions\.  | 2020\-03\-06 | 
| Wordpress application | `WordPressExploitableCommands_QUERYSTRING`  | New rule that checks for exploitable commands in the query string\. | 2020\-03\-03 | 
| Core Rule Set \(CRS\) | `SizeRestrictions_QUERYSTRING` `SizeRestrictions_Cookie_HEADER` `SizeRestrictions_BODY` `SizeRestrictions_URIPATH`  | Adjusted the size value constraints for improved accuracy\.  | 2020\-03\-03 | 
| SQL database | `SQLi_URIPATH`  | The rules now check the message URI\. | 2020\-01\-23 | 
| SQL database | `SQLi_BODY` `SQLi_QUERYARGUMENTS` `SQLi_COOKIE`  | Updated text transformations\. | 2019\-12\-20 | 
| Core Rule Set \(CRS\) | `CrossSiteScripting_URIPATH` `CrossSiteScripting_BODY` `CrossSiteScripting_QUERYARGUMENTS` `CrossSiteScripting_COOKIE`  | Updated text transformations\. | 2019\-12\-20 | 