# AWS Managed Rules Rule Groups List<a name="aws-managed-rule-groups-list"></a>

This section describes the AWS Managed Rules rule groups that are currently available\. You see these on the console when you add a managed rule group to your web ACL\. Through the API, you can retrieve this list along with the AWS Marketplace managed rule groups that you're subscribed to by calling `ListAvailableManagedRuleGroups`\. 

**Topics**
+ [Baseline Rule Groups](#aws-managed-rule-groups-baseline)
+ [Use\-Case Specific Rule Groups](#aws-managed-rule-groups-use-case)
+ [IP Reputation Rule Groups](#aws-managed-rule-groups-ip-rep)

## Baseline Rule Groups<a name="aws-managed-rule-groups-baseline"></a>

Baseline managed rule groups provide general protection against a wide variety of common threats\. Choose one or more of these rule groups to establish baseline protection for your resources\. 

**Core Rule Set \(CRS\)**  
VendorName: `AWS`, Name: `AWSManagedRulesCommonRuleSet`, WCU: 700

The Core Rule Set \(CRS\) rule group contains rules that are generally applicable to web applications\. This provides protection against exploitation of a wide range of vulnerabilities, including those described in OWASP publications and many Common Vulnerabilities and Exposures \(CVE\)\. Consider using this rule group for any AWS WAF use case\.

**Admin Protection**  
VendorName: `AWS`, Name: `AWSManagedRulesAdminProtectionRuleSet`, WCU: 100

The Admin Protection rule group contains rules that allow you to block external access to exposed administrative pages\. This might be useful if you run third\-party software or would like to reduce the risk of a malicious actor gaining administrative access to your application\.

**Known Bad Inputs**  
VendorName: `AWS`, Name: `AWSManagedRulesKnownBadInputsRuleSet`, WCU: 200

The Known Bad Inputs rule group contains rules to block request patterns that are known to be invalid and are associated with exploitation or discovery of vulnerabilities\. This can help reduce the risk of a malicious actor discovering a vulnerable application\.

## Use\-Case Specific Rule Groups<a name="aws-managed-rule-groups-use-case"></a>

Use case specific rule groups provide incremental protection for many diverse AWS WAF use cases\. Choose the rule groups that apply to your application\. 

**SQL Database**  
VendorName: `AWS`, Name: `AWSManagedRulesSQLiRuleSet`, WCU: 200

The SQL Database rule group contains rules to block request patterns associated with exploitation of SQL databases, like SQL injection attacks\. This can help prevent remote injection of unauthorized queries\. Evaluate this rule group for use if your application interfaces with an SQL database\.

**LINUX operating system**  
VendorName: `AWS`, Name: `AWSManagedRulesLinuxRuleSet`, WCU: 200

The Linux Operating System rule group contains rules that block request patterns associated with exploitation of vulnerabilities specific to Linux, including Linux\-specific Local File Inclusion \(LFI\) attacks\. This can help prevent attacks that expose file contents or execute code for which the attacker should not have had access\. You should evaluate this rule group if any part of your application runs on Linux\. You should use this rule group in conjunction with the POSIX Operating System rule group\. 

**POSIX Operating System**  
VendorName: `AWS`, Name: `AWSManagedRulesUnixRuleSet`, WCU: 100

The POSIX Operating System rule group contains rules that block request patterns associated with exploitation of vulnerabilities specific to POSIX and POSIX\-like operating systems, including Local File Inclusion \(LFI\) attacks\. This can help prevent attacks that expose file contents or execute code for which the attacker should not have had access\. You should evaluate this rule group if any part of your application runs on a POSIX or POSIX\-like operating system, including Linux, AIX, HP\-UX, macOS, Solaris, FreeBSD, OpenBSD, and many others\. 

**Windows Operating System**  
VendorName: `AWS`, Name: `AWSManagedRulesWindowsRuleSet`, WCU: 200

The Windows Operating System rule group contains rules that block request patterns associated with exploitation of vulnerabilities specific to Windows, like remote execution of PowerShell commands\. This can help prevent exploitation of vulnerabilities that allow an attacker to run unauthorized commands or execute malicious code\. Evaluate this rule group if any part of your application runs on a Windows operating system\.

**PHP Application**  
VendorName: `AWS`, Name: `AWSManagedRulesPHPRuleSet`, WCU: 100

The PHP Application rule group contains rules that block request patterns associated with the exploitation of vulnerabilities specific to the use of the PHP programming language, including injection of unsafe PHP functions\. This can help prevent exploitation of vulnerabilities that allow an attacker to remotely execute code or commands for which they are not authorized\. Evaluate this rule group if PHP is installed on any server with which your application interfaces\.

**WordPress Application**  
VendorName: `AWS`, Name: `AWSManagedRulesWordPressRuleSet`, WCU: 100

The WordPress Applications group contains rules that block request patterns associated with the exploitation of vulnerabilities specific to WordPress sites\. You should evaluate this rule group if you are running WordPress\. This rule group should be used in conjunction with the SQL Database and PHP Application rule groups\.

## IP Reputation Rule Groups<a name="aws-managed-rule-groups-ip-rep"></a>

IP reputation rule groups allow you to block requests based on their source\. Choose one or more of these rule groups if you would like to reduce your exposure to bot traffic, exploitation attempts, or if you are enforcing geographic restrictions on your content\. 

**Amazon IP Reputation**  
VendorName: `AWS`, Name: `AWSManagedRulesAmazonIpReputationList`, WCU: 25

This group contains rules that are based on Amazon internal threat intelligence\. This is useful if you would like to block IP addresses typically associated with bots or other threats\. Blocking these IP addresses can help mitigate bots and reduce the risk of a malicious actor discovering a vulnerable application\.