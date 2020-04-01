# AWS WAF rules<a name="waf-rules"></a>

In every rule group and every web ACL, rules define how to inspect web requests and what to do when a web request matches the inspection criteria\. Each rule requires one top\-level statement, which might contain nested statements at any depth, depending on the rule and statement type\. 

The inspection instructions are included in the JSON format as rule statements and the action in rule actions\. 

You use the rules in a web ACL to block or allow web requests based on criteria like the following: 
+ Scripts that are likely to be malicious\. Attackers embed scripts that can exploit vulnerabilities in web applications\. This is known as cross\-site scripting \(XSS\)\.
+ IP addresses or address ranges that requests originate from\.
+ Country or geographical location that requests originate from\.
+ Length of specified part of the request, such as the query string\.
+ SQL code that is likely to be malicious\. Attackers try to extract data from your database by embedding malicious SQL code in a web request\. This is known as SQL injection\.
+ Strings that appear in the request, for example, values that appear in the `User-Agent` header or text strings that appear in the query string\. You can also use regular expressions \(regex\) to specify these strings\.

Some rule types take multiple values\. For example, you can specify up to 10,000 IP addresses or IP address ranges in an IP address rule\.

In addition to statements like the ones in the preceding list, which provide web request inspection criteria, AWS WAF supports logical statements for AND, OR, and NOT that you use to combine statements in a rule\. 

For example, based on recent requests that you've seen from an attacker, you might create a rule with a logical AND statement that combines the following nested statements: 
+ The requests come from 192\.0\.2\.44\.
+ They contain the value `BadBot` in the `User-Agent` header\.
+ They appear to include SQL\-like code in the query string\.

In this case, all the statements need to result in a match for the top\-level AND statement to match\. 

Rules don't exist in AWS WAF on their own\. They aren't AWS resources, and they don't have Amazon Resource Names \(ARNs\)\. You can access a rule by name in the rule group or web ACL where it's defined\. You can manage rules and copy them to other web ACLs by using the JSON format of the rule group or web ACL that contains the rule\. Or you can manage them through the AWS WAF console **Rule Builder**, which is available for web ACLs and rule groups\.

**Topics**
+ [AWS WAF rule name](waf-rule-name.md)
+ [AWS WAF rule action](waf-rule-action.md)
+ [AWS WAF rule statements](waf-rule-statements.md)