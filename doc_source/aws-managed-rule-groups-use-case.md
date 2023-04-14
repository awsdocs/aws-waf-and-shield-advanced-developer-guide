# Use\-case specific rule groups<a name="aws-managed-rule-groups-use-case"></a>

Use\-case specific rule groups provide incremental protection for many diverse AWS WAF use cases\. Choose the rule groups that apply to your application\. 

## SQL database managed rule group<a name="aws-managed-rule-groups-use-case-sql-db"></a>

VendorName: `AWS`, Name: `AWSManagedRulesSQLiRuleSet`, WCU: 200

The SQL database rule group contains rules to block request patterns associated with exploitation of SQL databases, like SQL injection attacks\. This can help prevent remote injection of unauthorized queries\. Evaluate this rule group for use if your application interfaces with an SQL database\.

**Note**  
This table describes the latest static version of this rule group\. For other versions, use the API command [DescribeManagedRuleGroup](https://docs.aws.amazon.com/waf/latest/APIReference/API_DescribeManagedRuleGroup.html)\. 


| Rule name | Description and label | 
| --- | --- | 
| SQLi\_QUERYARGUMENTS |  Uses the built\-in AWS WAF [SQL injection attack rule statement](waf-rule-statement-type-sqli-match.md), with sensitivity level set to Low, to inspect the values of all query parameters for patterns that match malicious SQL code\.  Rule action: Block Label: `awswaf:managed:aws:sql-database:SQLi_QueryArguments`  | 
| SQLiExtendedPatterns\_QUERYARGUMENTS |  Inspects the values of all query parameters for patterns that match malicious SQL code\. The patterns this rule inspects for aren't covered by the rule `SQLi_QUERYARGUMENTS`\.  Rule action: Block `awswaf:managed:aws:sql-database:SQLiExtendedPatterns_QueryArguments`  | 
| SQLi\_BODY |  Uses the built\-in AWS WAF [SQL injection attack rule statement](waf-rule-statement-type-sqli-match.md), with sensitivity level set to Low, to inspect the request body for patterns that match malicious SQL code\.  This rule only inspects the request body up the body size limit for the web ACL\. The limit is 8 KB for regional web ACLs and 16 KB for CloudFront web ACLs\. For CloudFront web ACLs only, you can increase it up to 64 KB in your web ACL configuration\. This rule uses the `Continue` option for oversize content handling\. For more information, see [Handling oversize web request components](waf-oversize-request-components.md)\.  Rule action: Block Label: `awswaf:managed:aws:sql-database:SQLi_Body`  | 
| SQLiExtendedPatterns\_BODY |  Inspects the request body for patterns that match malicious SQL code\. The patterns this rule inspects for aren't covered by the rule `SQLi_BODY`\.  This rule only inspects the request body up the body size limit for the web ACL\. The limit is 8 KB for regional web ACLs and 16 KB for CloudFront web ACLs\. For CloudFront web ACLs only, you can increase it up to 64 KB in your web ACL configuration\. This rule uses the `Continue` option for oversize content handling\. For more information, see [Handling oversize web request components](waf-oversize-request-components.md)\.  Rule action: Block `awswaf:managed:aws:sql-database:SQLiExtendedPatterns_Body`  | 
| SQLi\_COOKIE |  Uses the built\-in AWS WAF [SQL injection attack rule statement](waf-rule-statement-type-sqli-match.md), with sensitivity level set to Low, to inspect the request cookie headers for patterns that match malicious SQL code\.  This rule only inspects the first 8 KB of the request cookies or the first 200 cookies, whichever limit is reached first, and it uses the `Continue` option for oversize content handling\. For more information, see [Handling oversize web request components](waf-oversize-request-components.md)\.  Rule action: Block Label: `awswaf:managed:aws:sql-database:SQLi_Cookie`  | 

## Linux operating system managed rule group<a name="aws-managed-rule-groups-use-case-linux-os"></a>

VendorName: `AWS`, Name: `AWSManagedRulesLinuxRuleSet`, WCU: 200

The Linux operating system rule group contains rules that block request patterns associated with the exploitation of vulnerabilities specific to Linux, including Linux\-specific Local File Inclusion \(LFI\) attacks\. This can help prevent attacks that expose file contents or run code for which the attacker should not have had access\. You should evaluate this rule group if any part of your application runs on Linux\. You should use this rule group in conjunction with the [POSIX operating system](#aws-managed-rule-groups-use-case-posix-os) rule group\.

**Note**  
This table describes the latest static version of this rule group\. For other versions, use the API command [DescribeManagedRuleGroup](https://docs.aws.amazon.com/waf/latest/APIReference/API_DescribeManagedRuleGroup.html)\. 


| Rule name | Description and label | 
| --- | --- | 
| LFI\_URIPATH |  Inspects the request path for attempts to exploit Local File Inclusion \(LFI\) vulnerabilities in web applications\. Example patterns include files like `/proc/version`, which could provide operating system information to attackers\.  Rule action: Block Label: `awswaf:managed:aws:linux-os:LFI_URIPath`  | 
| LFI\_QUERYSTRING |  Inspects the values of querystring for attempts to exploit Local File Inclusion \(LFI\) vulnerabilities in web applications\. Example patterns include files like `/proc/version`, which could provide operating system information to attackers\.  Rule action: Block Label: `awswaf:managed:aws:linux-os:LFI_QueryString`  | 
| LFI\_HEADER |  Inspects request headers for attempts to exploit Local File Inclusion \(LFI\) vulnerabilities in web applications\. Example patterns include files like `/proc/version`, which could provide operating system information to attackers\.  This rule only inspects the first 8 KB of the request headers or the first 200 headers, whichever limit is reached first, and it uses the `Continue` option for oversize content handling\. For more information, see [Handling oversize web request components](waf-oversize-request-components.md)\.  Rule action: Block Label: `awswaf:managed:aws:linux-os:LFI_Header`  | 

## POSIX operating system managed rule group<a name="aws-managed-rule-groups-use-case-posix-os"></a>

VendorName: `AWS`, Name: `AWSManagedRulesUnixRuleSet`, WCU: 100

The POSIX operating system rule group contains rules that block request patterns associated with the exploitation of vulnerabilities specific to POSIX and POSIX\-like operating systems, including Local File Inclusion \(LFI\) attacks\. This can help prevent attacks that expose file contents or run code for which the attacker should not have had access\. You should evaluate this rule group if any part of your application runs on a POSIX or POSIX\-like operating system, including Linux, AIX, HP\-UX, macOS, Solaris, FreeBSD, and OpenBSD\. 

**Note**  
This table describes the latest static version of this rule group\. For other versions, use the API command [DescribeManagedRuleGroup](https://docs.aws.amazon.com/waf/latest/APIReference/API_DescribeManagedRuleGroup.html)\. 


| Rule name | Description and label | 
| --- | --- | 
| UNIXShellCommandsVariables\_QUERYARGUMENTS |  Inspects the values of all query parameters for attempts to exploit command injection, LFI, and path traversal vulnerabilities in web applications that run on Unix systems\. Examples include patterns like `echo $HOME` and `echo $PATH`\.  Rule action: Block Label: `awswaf:managed:aws:posix-os:UNIXShellCommandsVariables_QUERYARGUMENTS`  | 
| UNIXShellCommandsVariables\_BODY |  Inspects the request body for attempts to exploit command injection, LFI, and path traversal vulnerabilities in web applications that run on Unix systems\. Examples include patterns like `echo $HOME` and `echo $PATH`\.  This rule only inspects the request body up the body size limit for the web ACL\. The limit is 8 KB for regional web ACLs and 16 KB for CloudFront web ACLs\. For CloudFront web ACLs only, you can increase it up to 64 KB in your web ACL configuration\. This rule uses the `Continue` option for oversize content handling\. For more information, see [Handling oversize web request components](waf-oversize-request-components.md)\.  Rule action: Block Label: `awswaf:managed:aws:posix-os:UNIXShellCommandsVariables_BODY`  | 

## Windows operating system managed rule group<a name="aws-managed-rule-groups-use-case-windows-os"></a>

VendorName: `AWS`, Name: `AWSManagedRulesWindowsRuleSet`, WCU: 200

The Windows operating system rule group contains rules that block request patterns associated with the exploitation of vulnerabilities specific to Windows, like remote execution of PowerShell commands\. This can help prevent exploitation of vulnerabilities that permit an attacker to run unauthorized commands or run malicious code\. Evaluate this rule group if any part of your application runs on a Windows operating system\.

**Note**  
This table describes the latest static version of this rule group\. For other versions, use the API command [DescribeManagedRuleGroup](https://docs.aws.amazon.com/waf/latest/APIReference/API_DescribeManagedRuleGroup.html)\. 


| Rule name | Description and label | 
| --- | --- | 
| WindowsShellCommands\_COOKIE |  Inspects the request cookie headers for WindowsShell command injection attempts in web applications\. The match patterns represent WindowsShell commands\. Example patterns include `\|\|nslookup` and `;cmd`\.  This rule only inspects the first 8 KB of the request cookies or the first 200 cookies, whichever limit is reached first, and it uses the `Continue` option for oversize content handling\. For more information, see [Handling oversize web request components](waf-oversize-request-components.md)\.  Rule action: Block Label: `awswaf:managed:aws:windows-os:WindowsShellCommands_Cookie`   | 
| WindowsShellCommands\_QUERYARGUMENTS |  Inspects the values of all query parameters for WindowsShell command injection attempts in web applications\. The match patterns represent WindowsShell commands\. Example patterns include `\|\|nslookup` and `;cmd`\.  Rule action: Block Label: `awswaf:managed:aws:windows-os:WindowsShellCommands_QueryArguments`   | 
| WindowsShellCommands\_BODY |  Inspects the request body for WindowsShell command injection attempts in web applications\. The match patterns represent WindowsShell commands\. Example patterns include `\|\|nslookup` and `;cmd`\.  This rule only inspects the request body up the body size limit for the web ACL\. The limit is 8 KB for regional web ACLs and 16 KB for CloudFront web ACLs\. For CloudFront web ACLs only, you can increase it up to 64 KB in your web ACL configuration\. This rule uses the `Continue` option for oversize content handling\. For more information, see [Handling oversize web request components](waf-oversize-request-components.md)\.  Rule action: Block Label: `awswaf:managed:aws:windows-os:WindowsShellCommands_Body`   | 
| PowerShellCommands\_COOKIE |  Inspects the request cookie headers for PowerShell command injection attempts in web applications\. The match patterns represent PowerShell commands\. For example, `Invoke-Expression`\.  This rule only inspects the first 8 KB of the request cookies or the first 200 cookies, whichever limit is reached first, and it uses the `Continue` option for oversize content handling\. For more information, see [Handling oversize web request components](waf-oversize-request-components.md)\.  Rule action: Block Label: `awswaf:managed:aws:windows-os:PowerShellCommands_Cookie`  | 
| PowerShellCommands\_QUERYARGUMENTS |  Inspects the values of all query parameters for PowerShell command injection attempts in web applications\. The match patterns represent PowerShell commands\. For example, `Invoke-Expression`\.  Rule action: Block Label: `awswaf:managed:aws:windows-os:PowerShellCommands_QueryArguments`  | 
| PowerShellCommands\_BODY |  Inspects the request body for PowerShell command injection attempts in web applications\. The match patterns represent PowerShell commands\. For example, `Invoke-Expression`\.  This rule only inspects the request body up the body size limit for the web ACL\. The limit is 8 KB for regional web ACLs and 16 KB for CloudFront web ACLs\. For CloudFront web ACLs only, you can increase it up to 64 KB in your web ACL configuration\. This rule uses the `Continue` option for oversize content handling\. For more information, see [Handling oversize web request components](waf-oversize-request-components.md)\.  Rule action: Block Label: `awswaf:managed:aws:windows-os:PowerShellCommands_Body`   | 

## PHP application managed rule group<a name="aws-managed-rule-groups-use-case-php-app"></a>

VendorName: `AWS`, Name: `AWSManagedRulesPHPRuleSet`, WCU: 100

The PHP application rule group contains rules that block request patterns associated with the exploitation of vulnerabilities specific to the use of the PHP programming language, including injection of unsafe PHP functions\. This can help prevent exploitation of vulnerabilities that permit an attacker to remotely run code or commands for which they are not authorized\. Evaluate this rule group if PHP is installed on any server with which your application interfaces\.

**Note**  
This table describes the latest static version of this rule group\. For other versions, use the API command [DescribeManagedRuleGroup](https://docs.aws.amazon.com/waf/latest/APIReference/API_DescribeManagedRuleGroup.html)\. 


| Rule name | Description and label | 
| --- | --- | 
| PHPHighRiskMethodsVariables\_HEADER |  Inspects all headers for PHP script code injection attempts\. Example patterns include functions like `fsockopen` and the `$_GET` superglobal variable\.  This rule only inspects the first 8 KB of the request headers or the first 200 headers, whichever limit is reached first, and it uses the `Continue` option for oversize content handling\. For more information, see [Handling oversize web request components](waf-oversize-request-components.md)\.  Rule action: Block Label: `awswaf:managed:aws:php-app:PHPHighRiskMethodsVariables_Header`  | 
| PHPHighRiskMethodsVariables\_QUERYSTRING |  Inspects everything after the first `?` in the request URL, looking for PHP script code injection attempts\. Example patterns include functions like `fsockopen` and the `$_GET` superglobal variable\.  Rule action: Block Label: `awswaf:managed:aws:php-app:PHPHighRiskMethodsVariables_QueryString`  | 
| PHPHighRiskMethodsVariables\_BODY |  Inspects the values of the request body for PHP script code injection attempts\. Example patterns include functions like `fsockopen` and the `$_GET` superglobal variable\.  This rule only inspects the request body up the body size limit for the web ACL\. The limit is 8 KB for regional web ACLs and 16 KB for CloudFront web ACLs\. For CloudFront web ACLs only, you can increase it up to 64 KB in your web ACL configuration\. This rule uses the `Continue` option for oversize content handling\. For more information, see [Handling oversize web request components](waf-oversize-request-components.md)\.  Rule action: Block Label: `awswaf:managed:aws:php-app:PHPHighRiskMethodsVariables_Body`  | 

## WordPress application managed rule group<a name="aws-managed-rule-groups-use-case-wordpress-app"></a>

VendorName: `AWS`, Name: `AWSManagedRulesWordPressRuleSet`, WCU: 100

The WordPress application rule group contains rules that block request patterns associated with the exploitation of vulnerabilities specific to WordPress sites\. You should evaluate this rule group if you are running WordPress\. This rule group should be used in conjunction with the [SQL database](#aws-managed-rule-groups-use-case-sql-db) and [PHP application](#aws-managed-rule-groups-use-case-php-app) rule groups\.

**Note**  
This table describes the latest static version of this rule group\. For other versions, use the API command [DescribeManagedRuleGroup](https://docs.aws.amazon.com/waf/latest/APIReference/API_DescribeManagedRuleGroup.html)\. 


| Rule name | Description and label | 
| --- | --- | 
| WordPressExploitableCommands\_QUERYSTRING |  Inspects the request query string for high risk WordPress commands that can be exploited in vulnerable installations or plugins\. Examples patterns include commands like `do-reset-wordpress`\.  Rule action: Block Label: `awswaf:managed:aws:wordpress-app:WordPressExploitableCommands_QUERYSTRING`  | 
| WordPressExploitablePaths\_URIPATH |  Inspects the request URI path for WordPress files like `xmlrpc.php`, which are known to have easily exploitable vulnerabilities\.  Rule action: Block Label: `awswaf:managed:aws:wordpress-app:WordPressExploitablePaths_URIPATH`  | 