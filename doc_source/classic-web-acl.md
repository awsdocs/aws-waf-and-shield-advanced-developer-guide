# Creating and configuring a Web Access Control List \(Web ACL\)<a name="classic-web-acl"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

A web access control list \(web ACL\) gives you fine\-grained control over the web requests that your Amazon API Gateway API, Amazon CloudFront distribution or Application Load Balancer responds to\. You can allow or block the following types of requests: 
+ Originate from an IP address or a range of IP addresses
+ Originate from a specific country or countries
+ Contain a specified string or match a regular expression \(regex\) pattern in a particular part of requests
+ Exceed a specified length
+ Appear to contain malicious SQL code \(known as SQL injection\)
+ Appear to contain malicious scripts \(known as cross\-site scripting\)

You can also test for any combination of these conditions, or block or count web requests that not only meet the specified conditions, but also exceed a specified number of requests in any 5\-minute period\. 

To choose the requests that you want to allow to have access to your content or that you want to block, perform the following tasks:

1. Choose the default action, allow or block, for web requests that don't match any of the conditions that you specify\. For more information, see [Deciding on the default action for a Web ACL](classic-web-acl-default-action.md)\.

1. Specify the conditions under which you want to allow or block requests:
   + To allow or block requests based on whether the requests appear to contain malicious scripts, create cross\-site scripting match conditions\. For more information, see [Working with cross\-site scripting match conditions](classic-web-acl-xss-conditions.md)\.
   + To allow or block requests based on the IP addresses that they originate from, create IP match conditions\. For more information, see [Working with IP match conditions](classic-web-acl-ip-conditions.md)\.
   + To allow or block requests based on the country that they originate from, create geo match conditions\. For more information, see [Working with geographic match conditions](classic-web-acl-geo-conditions.md)\.
   + To allow or block requests based on whether the requests exceed a specified length, create size constraint conditions\. For more information, see [Working with size constraint conditions](classic-web-acl-size-conditions.md)\.
   + To allow or block requests based on whether the requests appear to contain malicious SQL code, create SQL injection match conditions\. For more information, see [Working with SQL injection match conditions](classic-web-acl-sql-conditions.md)\.
   + To allow or block requests based on strings that appear in the requests, create string match conditions\. For more information, see [Working with string match conditions](classic-web-acl-string-conditions.md)\.
   + To allow or block requests based on a regex pattern that appear in the requests, create regex match conditions\. For more information, see [Working with regex match conditions](classic-web-acl-regex-conditions.md)\.

1. Add the conditions to one or more rules\. If you add more than one condition to the same rule, web requests must match all the conditions for AWS WAF Classic to allow or block requests based on the rule\. For more information, see [Working with rules](classic-web-acl-rules.md)\. Optionally, you can use a rate\-based rule instead of a regular rule to limit the number of requests from any IP address that meets the conditions\.

1. Add the rules to a web ACL\. For each rule, specify whether you want AWS WAF Classic to allow or block requests based on the conditions that you added to the rule\. If you add more than one rule to a web ACL, AWS WAF Classic evaluates the rules in the order that they're listed in the web ACL\. For more information, see [Working with web ACLs](classic-web-acl-working-with.md)\.

   When you add a new rule or update existing rules, it can take up to one minute for those changes to appear and be active across your web ACLs and resources\.

**Topics**
+ [Working with conditions](classic-web-acl-create-condition.md)
+ [Working with rules](classic-web-acl-rules.md)
+ [Working with web ACLs](classic-web-acl-working-with.md)