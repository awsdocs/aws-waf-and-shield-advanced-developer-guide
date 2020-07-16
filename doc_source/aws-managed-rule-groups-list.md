# AWS Managed Rules rule groups list<a name="aws-managed-rule-groups-list"></a>

This section describes the AWS Managed Rules rule groups that are currently available\. You see these on the console when you add a managed rule group to your web ACL\. Through the API, you can retrieve this list along with the AWS Marketplace managed rule groups that you're subscribed to by calling `ListAvailableManagedRuleGroups`\. 

**Topics**
+ [Baseline rule groups](#aws-managed-rule-groups-baseline)
+ [Use\-case specific rule groups](#aws-managed-rule-groups-use-case)
+ [IP reputation rule groups](#aws-managed-rule-groups-ip-rep)

## Baseline rule groups<a name="aws-managed-rule-groups-baseline"></a>

Baseline managed rule groups provide general protection against a wide variety of common threats\. Choose one or more of these rule groups to establish baseline protection for your resources\.

**Core rule set \(CRS\)**  
VendorName: `AWS`, Name: `AWSManagedRulesCommonRuleSet`, WCU: 700

The Core rule set \(CRS\) rule group contains rules that are generally applicable to web applications\. This provides protection against exploitation of a wide range of vulnerabilities, including high risk and commonly occurring vulnerabilities described in OWASP publications\. Consider using this rule group for any AWS WAF use case\.


| Rule name | Description | 
| --- | --- | 
| NoUserAgent\_HEADER | Blocks requests with no HTTP User\-Agent header\. | 
| UserAgent\_BadBots\_HEADER | Inspects for the presence of common User\-Agent header values indicating the request to be a bad bot\. Example patterns include nessus, and nmap\. | 
| SizeRestrictions\_QUERYSTRING | Verifies that the URI query string length is within the standard boundary for applications\.  | 
| SizeRestrictions\_Cookie\_HEADER | Verifies that the cookie header length is within the bounds common for many applications\.  | 
| SizeRestrictions\_BODY | Verifies that the request body size is within the bounds common for many applications\.  | 
| SizeRestrictions\_URIPATH | Verifies that the URI path length is within specification\. | 
| EC2MetaDataSSRF\_BODY | Inspects for attempts to exfiltrate Amazon EC2 metadata from the request body\. | 
| EC2MetaDataSSRF\_COOKIE | Inspects for attempts to exfiltrate Amazon EC2 metadata from the request cookie\. | 
| EC2MetaDataSSRF\_URIPATH | Inspects for attempts to exfiltrate Amazon EC2 metadata from the request URI path\. | 
| EC2MetaDataSSRF\_QUERYARGUMENTS | Inspects for attempts to exfiltrate Amazon EC2 metadata from the request query arguments\. | 
| GenericLFI\_QUERYARGUMENTS | Inspects for the presence of Local File Inclusion \(LFI\) exploits in the query arguments\. Examples include path traversal attempts using techniques like \.\./\.\./\. | 
| GenericLFI\_URIPATH | Inspects for the presence of Local File Inclusion \(LFI\) exploits in the URI path\. Examples include path traversal attempts using techniques like \.\./\.\./\. | 
| GenericLFI\_BODY | Inspects for the presence of Local File Inclusion \(LFI\) exploits in the request body\. Examples include path traversal attempts using techniques like \.\./\.\./\. | 
| RestrictedExtensions\_URIPATH | Inspects requests whose URI path includes system file extensions that the clients shouldn't read or run\. Example patterns include extensions like \.log and \.ini\. | 
| RestrictedExtensions\_QUERYARGUMENTS | Inspects requests whose query arguments are system file extensions that the clients shouldn't read or run\. Example patterns include extensions like \.log and \.ini\. | 
| GenericRFI\_QUERYARGUMENTS | Inspects the values of all query parameters and blocks requests attempting to exploit RFI \(Remote File Inclusion\) in web applications\. Examples include patterns like ://\. | 
| GenericRFI\_BODY | Inspects the values of the request body and blocks requests attempting to exploit RFI \(Remote File Inclusion\) in web applications\. Examples include patterns like ://\. | 
| GenericRFI\_URIPATH | Inspects the values of the URI path and blocks requests attempting to exploit RFI \(Remote File Inclusion\) in web applications\. Examples include patterns like ://\. | 
| CrossSiteScripting\_COOKIE | Inspects the value of cookie headers and blocks common cross\-site scripting \(XSS\) patterns using the built\-in XSS detection rule in AWS WAF\. Example patterns include scripts like <script>alert\("hello"\)</script>\. | 
| CrossSiteScripting\_QUERYARGUMENTS | Inspects the value of query arguments and blocks common cross\-site scripting \(XSS\) patterns using the built\-in XSS detection rule in AWS WAF\. Example patterns include scripts like <script>alert\("hello"\)</script>\. | 
| CrossSiteScripting\_BODY | Inspects the value of the request body and blocks common cross\-site scripting \(XSS\) patterns using the built\-in XSS detection rule in AWS WAF\. Example patterns include scripts like <script>alert\("hello"\)</script>\. | 
| CrossSiteScripting\_URIPATH | Inspects the value of the URI path and blocks common cross\-site scripting \(XSS\) patterns using the built\-in XSS detection rule in AWS WAF\. Example patterns include scripts like <script>alert\("hello"\)</script>\. | 

**Admin protection**  
VendorName: `AWS`, Name: `AWSManagedRulesAdminProtectionRuleSet`, WCU: 100

The Admin protection rule group contains rules that allow you to block external access to exposed administrative pages\. This might be useful if you run third\-party software or want to reduce the risk of a malicious actor gaining administrative access to your application\.


| Rule name | Description | 
| --- | --- | 
| AdminProtection\_URIPATH | Inspects requests for URI paths that are generally reserved for administration of a webserver or application\. Example patterns include sqlmanager\. | 

**Known bad inputs**  
VendorName: `AWS`, Name: `AWSManagedRulesKnownBadInputsRuleSet`, WCU: 200

The Known bad inputs rule group contains rules to block request patterns that are known to be invalid and are associated with exploitation or discovery of vulnerabilities\. This can help reduce the risk of a malicious actor discovering a vulnerable application\.


| Rule name | Description | 
| --- | --- | 
| Host\_localhost\_HEADER | Inspects the host header in the request for patterns indicating localhost\. Example patterns include localhost\. | 
| PROPFIND\_METHOD | Inspects the HTTP method in the request for PROPFIND, which is a method similar to HEAD, but with the extra intention to exfiltrate XML objects\. | 
| ExploitablePaths\_URIPATH | Inspects the URI path for attempts to access exploitable web application paths\. Example patterns include paths like web\-inf\. | 
| BadAuthToken\_COOKIE\_AUTHORIZATION | Inspects the request for the presence of an unsolicited JSON Web Token \(JWT\)\. This protects against a malicious actor attempting to guess the secret key\. | 

## Use\-case specific rule groups<a name="aws-managed-rule-groups-use-case"></a>

Use\-case specific rule groups provide incremental protection for many diverse AWS WAF use cases\. Choose the rule groups that apply to your application\. 

**SQL database**  
VendorName: `AWS`, Name: `AWSManagedRulesSQLiRuleSet`, WCU: 200

The SQL database rule group contains rules to block request patterns associated with exploitation of SQL databases, like SQL injection attacks\. This can help prevent remote injection of unauthorized queries\. Evaluate this rule group for use if your application interfaces with an SQL database\.


| Rule name | Description | 
| --- | --- | 
| SQLiExtendedPatterns\_QUERYARGUMENTS | Inspects the values of all query parameters for patterns that match malicious SQL code\. The patterns this rule inspects for aren't covered by the built\-in AWS WAF SQL injection match statement\. | 
| SQLi\_QUERYARGUMENTS | Uses the built\-in AWS WAF SQL injection match statement to inspect the values of all query parameters for patterns that match malicious SQL code\.  | 
| SQLi\_BODY | Uses the built\-in AWS WAF SQL injection match statement to inspect the request body for patterns that match malicious SQL code\. | 
| SQLi\_COOKIE | Uses the built\-in AWS WAF SQL injection match statement to inspect the request cookie header for patterns that match malicious SQL code\.  | 
| SQLi\_URIPATH | Uses the built\-in AWS WAF injection match statement to inspect the request URI path for patterns that match malicious SQL code\.  | 

**Linux operating system**  
VendorName: `AWS`, Name: `AWSManagedRulesLinuxRuleSet`, WCU: 200

The Linux operating system rule group contains rules that block request patterns associated with the exploitation of vulnerabilities specific to Linux, including Linux\-specific Local File Inclusion \(LFI\) attacks\. This can help prevent attacks that expose file contents or run code for which the attacker should not have had access\. You should evaluate this rule group if any part of your application runs on Linux\. You should use this rule group in conjunction with the [POSIX operating system](#posix_os) rule group\. 


| Rule name | Description | 
| --- | --- | 
| LFI\_URIPATH | Inspects the request path for attempts to exploit Local File Inclusion \(LFI\) vulnerabilities in web applications\. Example patterns include files like /proc/version, which could provide operating system information to attackers\. | 
| LFI\_QUERYARGUMENTS | Inspects the values of all query parameters for attempts to exploit Local File Inclusion \(LFI\) vulnerabilities in web applications\. Example patterns include files like /proc/version, which could provide operating system information to attackers\. | 
| LFI\_BODY | Inspects the request body for attempts to exploit Local File Inclusion \(LFI\) vulnerabilities in web applications\. Example patterns include files like /proc/version, which could provide operating system information to attackers\. | 

**POSIX operating system**  
VendorName: `AWS`, Name: `AWSManagedRulesUnixRuleSet`, WCU: 100

The POSIX operating system rule group contains rules that block request patterns associated with the exploitation of vulnerabilities specific to POSIX and POSIX\-like operating systems, including Local File Inclusion \(LFI\) attacks\. This can help prevent attacks that expose file contents or run code for which the attacker should not have had access\. You should evaluate this rule group if any part of your application runs on a POSIX or POSIX\-like operating system, including Linux, AIX, HP\-UX, macOS, Solaris, FreeBSD, and OpenBSD\. 


| Rule name | Description | 
| --- | --- | 
| UNIXShellCommandsVariables\_QUERYARGUMENTS | Inspects the values of all query parameters for attempts to exploit command injection, LFI, and path traversal vulnerabilities in web applications that run on Unix systems\. Examples include patterns like echo $HOME and echo $PATH\. | 
| UNIXShellCommandsVariables\_BODY | Inspects the request body for attempts to exploit command injection, LFI, and path traversal vulnerabilities in web applications that run on Unix systems\. Examples include patterns like echo $HOME and echo $PATH\. | 

**Windows operating system**  
VendorName: `AWS`, Name: `AWSManagedRulesWindowsRuleSet`, WCU: 200

The Windows operating system rule group contains rules that block request patterns associated with the exploitation of vulnerabilities specific to Windows, like remote execution of PowerShell commands\. This can help prevent exploitation of vulnerabilities that allow an attacker to run unauthorized commands or run malicious code\. Evaluate this rule group if any part of your application runs on a Windows operating system\.


| Rule name | Description | 
| --- | --- | 
| PowerShellCommands\_Set1\_QUERYARGUMENTS | Inspects the values of all query parameters and blocks PowerShell command injection attempts in web applications\. Example patterns include functions like Invoke\-Expression\. | 
| PowerShellCommands\_Set2\_QUERYARGUMENTS | Inspects the values of all query parameters and blocks PowerShell command injection attempts in web applications\. Example patterns include functions like Invoke\-Expression\. | 
| PowerShellCommands\_Set1\_BODY | Inspects the request body and blocks PowerShell command injection attempts in web applications\. Example patterns include functions like Invoke\-Expression\. | 
| PowerShellCommands\_Set2\_BODY | Inspects the request body and blocks PowerShell command injection attempts in web applications\. Example patterns include functions like Invoke\-Expression\. | 

**PHP application**  
VendorName: `AWS`, Name: `AWSManagedRulesPHPRuleSet`, WCU: 100

The PHP application rule group contains rules that block request patterns associated with the exploitation of vulnerabilities specific to the use of the PHP programming language, including injection of unsafe PHP functions\. This can help prevent exploitation of vulnerabilities that allow an attacker to remotely run code or commands for which they are not authorized\. Evaluate this rule group if PHP is installed on any server with which your application interfaces\.


| Rule name | Description | 
| --- | --- | 
| PHPHighRiskMethodsVariables\_QUERYARGUMENTS | Inspects the values of all query parameters for PHP script code injection attempts\. Example patterns include functions like fsockopen and the $\_GET superglobal variable\. | 
| PHPHighRiskMethodsVariables\_BODY | Inspects the values of the request body for PHP script code injection attempts\. Example patterns include functions like fsockopen and the $\_GET superglobal variable\. | 

**WordPress application**  
VendorName: `AWS`, Name: `AWSManagedRulesWordPressRuleSet`, WCU: 100

The WordPress application rule group contains rules that block request patterns associated with the exploitation of vulnerabilities specific to WordPress sites\. You should evaluate this rule group if you are running WordPress\. This rule group should be used in conjunction with the [SQL database](#sql_db) and [PHP application](#php_app) rule groups\.


| Rule name | Description | 
| --- | --- | 
| WordPressExploitableCommands\_QUERYSTRING | Inspects the request query string for high risk WordPress commands that can be exploited in vulnerable installations or plugins\. Examples patterns include commands like do\-reset\-wordpress\. | 
| WordPressExploitablePaths\_URIPATH | Inspects the request URI path for WordPress files like xmlrpc\.php, which are known to have easily exploitable vulnerabilities\.  | 

## IP reputation rule groups<a name="aws-managed-rule-groups-ip-rep"></a>

IP reputation rule groups allow you to block requests based on their source\. Choose one or more of these rule groups if you want to reduce your exposure to bot traffic or exploitation attempts, or if you are enforcing geographic restrictions on your content\. 

**Amazon IP reputation list**  
VendorName: `AWS`, Name: `AWSManagedRulesAmazonIpReputationList`, WCU: 25

The Amazon IP reputation list rule group contains rules that are based on Amazon internal threat intelligence\. This is useful if you would like to block IP addresses typically associated with bots or other threats\. Blocking these IP addresses can help mitigate bots and reduce the risk of a malicious actor discovering a vulnerable application\.


| Rule name | Description | 
| --- | --- | 
| AWSManagedIPReputationList\_xxxx | Inspects for a list of IP addresses that have been identified as malicious actors and bots by Amazon threat intelligence\. | 

**Anonymous IP list**  
VendorName: `AWS`, Name: `AWSManagedRulesAnonymousIpList`, WCU: 50

The Anonymous IP list rule group contains rules to block requests from services that allow the obfuscation of viewer identity\. These include requests from VPNs, proxies, Tor nodes, and hosting providers \(including AWS\)\. This rule group is useful if you want to filter out viewers that might be trying to hide their identity from your application\. Blocking the IP addresses of these services can help mitigate bots and evasion of geographic restrictions\.


| Rule name | Description | 
| --- | --- | 
| AnonymousIPList | Inspects for a list of IP addresses of sources known to anonymize client information, like TOR nodes, temporary proxies, and other masking services\.  | 
| HostingProviderIPList | Inspects for a list of IP addresses from hosting and cloud providers, which are less likely to source end\-user traffic\. Examples include cloud providers like AWS\. | 