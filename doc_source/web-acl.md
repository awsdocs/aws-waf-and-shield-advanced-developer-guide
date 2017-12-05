# Creating and Configuring a Web Access Control List \(Web ACL\)<a name="web-acl"></a>

A web access control list \(web ACL\) gives you fine\-grained control over the web requests that your Amazon CloudFront distributions or Application Load Balancers respond to\. You can allow or block the following types of requests: 

+ Originate from an IP address or a range of IP addresses

+ Originate from a specific country or countries

+ Contain a specified string or match a regular expression \(regex\) pattern in a particular part of requests

+ Exceed a specified length

+ Appear to contain malicious SQL code \(known as SQL injection\)

+ Appear to contain malicious scripts \(known as cross\-site scripting\)

You can also test for any combination of these conditions, or block or count web requests that not only meet the specified conditions, but also exceed a specified number of requests in any 5\-minute period\. 

To choose the requests that you want to allow to have access to your content or that you want to block, perform the following tasks:

1. Choose the default action, allow or block, for web requests that don't match any of the conditions that you specify\. For more information, see [Deciding on the Default Action for a Web ACL](web-acl-default-action.md)\.

1. Specify the conditions under which you want to allow or block requests:

   + To allow or block requests based on whether the requests appear to contain malicious scripts, create cross\-site scripting match conditions\. For more information, see [Working with Cross\-site Scripting Match Conditions](web-acl-xss-conditions.md)\.

   + To allow or block requests based on the IP addresses that they originate from, create IP match conditions\. For more information, see [Working with IP Match Conditions](web-acl-ip-conditions.md)\.

   + To allow or block requests based on the country that they originate from, create geo match conditions\. For more information, see [Working with Geographic Match Conditions](web-acl-geo-conditions.md)\.

   + To allow or block requests based on whether the requests exceed a specified length, create size constraint conditions\. For more information, see [Working with Size Constraint Conditions](web-acl-size-conditions.md)\.

   + To allow or block requests based on whether the requests appear to contain malicious SQL code, create SQL injection match conditions\. For more information, see [Working with SQL Injection Match Conditions](web-acl-sql-conditions.md)\.

   + To allow or block requests based on strings that appear in the requests, create string match conditions\. For more information, see [Working with String Match Conditions](web-acl-string-conditions.md)\.

   + To allow or block requests based on a regex pattern that appear in the requests, create regex match conditions\. For more information, see [Working with Regex Match Conditions](web-acl-regex-conditions.md)\.

1. Add the conditions to one or more rules\. If you add more than one condition to the same rule, web requests must match all the conditions for AWS WAF to allow or block requests based on the rule\. For more information, see [Working with Rules](web-acl-rules.md)\. Optionally, also add a rate limit to the rule, which specifies the maximum number of requests that are allowed from a specific IP address\.

1. Add the rules to a web ACL\. For each rule, specify whether you want AWS WAF to allow or block requests based on the conditions that you added to the rule\. If you add more than one rule to a web ACL, AWS WAF evaluates the rules in the order that they're listed in the web ACL\. For more information, see [Working with Web ACLs](web-acl-working-with.md)\.


+ [Working with conditions](web-acl-create-condition.md)
+ [Working with Rules](web-acl-rules.md)
+ [Working with Web ACLs](web-acl-working-with.md)