# AWS Managed Rules changelog<a name="aws-managed-rule-groups-changelog"></a>

This section lists changes to the AWS Managed Rules for AWS WAF since their release in November, 2019\.

**Note**  
This changelog reports changes to the rules and rule groups in AWS Managed Rules for AWS WAF\. It doesn't report changes to the IP address lists that are used by the rules in the [IP reputation rule groups](aws-managed-rule-groups-list.md#aws-managed-rule-groups-ip-rep), due to the dynamic nature of those lists\.


| Rule group | Rules affected | Description | Date | 
| --- | --- | --- | --- | 
| Core rule set AWSManagedRulesCommonRuleSet |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-changelog.html)  | Changed the text transformation from HTML decode to URL decode, to improve blocking\.  | Aug 07, 2020 | 
| Linux operating system |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-changelog.html)  | Changed the text transformation from HTML entity decode to URL decode, to improve detection and blocking\.  | May 19, 2020 | 
| Anonymous IP List | All | New rule group in [IP reputation rule groups](aws-managed-rule-groups-list.md#aws-managed-rule-groups-ip-rep) to block requests from services that allow the obfuscation of viewer identity, to help mitigate bots and evasion of geographic restrictions\.  | March 06, 2020 | 
| Wordpress application | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-changelog.html) | New rule that checks for exploitable commands in the query string\. | March 03, 2020 | 
| Core Rule Set \(CRS\) | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-changelog.html) | Adjusted the size value constraints for improved accuracy\.  | March 03, 2020 | 
| SQL database |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-changelog.html)  | The rules now check the message URI\. | January 23, 2020 | 
| SQL database | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-changelog.html) | Updated text transformations\. | December 20, 2019 | 
| Core Rule Set \(CRS\) | [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-changelog.html)  | Updated text transformations\. | December 20, 2019 | 