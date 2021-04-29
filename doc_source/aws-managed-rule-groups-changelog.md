# AWS Managed Rules changelog<a name="aws-managed-rule-groups-changelog"></a>

This section lists changes to the AWS Managed Rules for AWS WAF since their release in November, 2019\.

**Note**  
This changelog reports changes to the rules and rule groups in AWS Managed Rules for AWS WAF\. It doesn't report changes to the IP address lists that are used by the rules in the [IP reputation rule groups](aws-managed-rule-groups-list.md#aws-managed-rule-groups-ip-rep), due to the dynamic nature of those lists\.


| Rule group | Rules affected | Description | Date | 
| --- | --- | --- | --- | 
| AWS WAF Bot Control | All | Added the Bot Control rule set\.  | 2021\-04\-01 | 
| Core rule set \(CRS\) | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-changelog.html) | Added double URL decode\.  | 2021\-03\-03 | 
| Core rule set \(CRS\) | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-changelog.html) | Improved the configuration of the rules and added an extra URL decode\.  | 2021\-03\-03 | 
| Admin protection | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-changelog.html) | Added double URL decode\.  | 2021\-03\-03 | 
| Known bad inputs | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-changelog.html) | Improved the configuration of the rules and added an extra URL decode\.  | 2021\-03\-03 | 
| Linux operating system | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-changelog.html) | Improved the configuration of the rules and added an extra URL decode\.  | 2021\-03\-03 | 
| Windows operating system | All | Improved the configuration of the rules\.  | 2020\-09\-23 | 
| PHP application |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-changelog.html)  | Changed the text transformation from HTML decode to URL decode, to improve blocking\.  | 2020\-09\-16 | 
| POSIX operating system |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-changelog.html)  | Changed the text transformation from HTML decode to URL decode, to improve blocking\.  | 2020\-09\-16 | 
| Core rule set |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-changelog.html)  | Changed the text transformation from HTML decode to URL decode, to improve blocking\.  | 2020\-08\-07 | 
| Linux operating system |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-changelog.html)  | Changed the text transformation from HTML entity decode to URL decode, to improve detection and blocking\.  | 2020\-05\-19 | 
| Anonymous IP List | All | New rule group in [IP reputation rule groups](aws-managed-rule-groups-list.md#aws-managed-rule-groups-ip-rep) to block requests from services that allow the obfuscation of viewer identity, to help mitigate bots and evasion of geographic restrictions\.  | 2020\-03\-06 | 
| Wordpress application | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-changelog.html) | New rule that checks for exploitable commands in the query string\. | 2020\-03\-03 | 
| Core Rule Set \(CRS\) | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-changelog.html) | Adjusted the size value constraints for improved accuracy\.  | 2020\-03\-03 | 
| SQL database |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-changelog.html)  | The rules now check the message URI\. | 2020\-01\-23 | 
| SQL database | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-changelog.html) | Updated text transformations\. | 2019\-12\-20 | 
| Core Rule Set \(CRS\) | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-changelog.html)  | Updated text transformations\. | 2019\-12\-20 | 