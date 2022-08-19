# Rules<a name="waf-rules"></a>

An AWS WAF rule defines how to inspect HTTP\(S\) web requests and the action to take on a request when it matches the inspection criteria\. You define rules only in the context of a rule group or web ACL\. 

You can define rules that inspect for criteria like the following: 
+ Scripts that are likely to be malicious\. Attackers embed scripts that can exploit vulnerabilities in web applications\. This is known as cross\-site scripting \(XSS\)\.
+ IP addresses or address ranges that requests originate from\.
+ Country or geographical location that requests originate from\.
+ Length of a specified part of the request, such as the query string\.
+ SQL code that is likely to be malicious\. Attackers try to extract data from your database by embedding malicious SQL code in a web request\. This is known as SQL injection\.
+ Strings that appear in the request, for example, values that appear in the `User-Agent` header or text strings that appear in the query string\. You can also use regular expressions \(regex\) to specify these strings\.
+ Labels that prior rules in the web ACL have added to the request\.

Each rule requires one top\-level statement, which might contain nested statements at any depth, depending on the rule and statement type\. Some rule types take sets of criteria\. For example, you can specify up to 10,000 IP addresses or IP address ranges in an IP address rule\.

In addition to statements with web request inspection criteria, like the ones in the preceding list, AWS WAF supports logical statements for `AND`, `OR`, and `NOT` that you use to combine statements in a rule\. 

For example, based on recent requests that you've seen from an attacker, you might create a rule with a logical `AND` statement that combines the following nested statements: 
+ The requests come from 192\.0\.2\.44\.
+ They contain the value `BadBot` in the `User-Agent` header\.
+ They appear to include SQL\-like code in the query string\.

In this case, the web request needs to match all of the statements to result in a match for the top\-level `AND`\. 

Rules don't exist in AWS WAF on their own\. They aren't AWS resources, and they don't have Amazon Resource Names \(ARNs\)\. You can access a rule by name in the rule group or web ACL where it's defined\. You can manage rules and copy them to other web ACLs by using the JSON format of the rule group or web ACL that contains the rule\. Or you can manage them through the AWS WAF console **Rule Builder**, which is available for web ACLs and rule groups\.

**Topics**
+ [AWS WAF rule name](waf-rule-name.md)
+ [AWS WAF rule action](waf-rule-action.md)
+ [AWS WAF rule statements](waf-rule-statements.md)