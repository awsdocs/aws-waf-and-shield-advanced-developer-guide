# Working with conditions<a name="classic-web-acl-create-condition"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

Conditions specify when you want to allow or block requests\.
+ To allow or block requests based on whether the requests appear to contain malicious scripts, create cross\-site scripting match conditions\. For more information, see [Working with cross\-site scripting match conditions](classic-web-acl-xss-conditions.md)\.
+ To allow or block requests based on the IP addresses that they originate from, create IP match conditions\. For more information, see [Working with IP match conditions](classic-web-acl-ip-conditions.md)\.
+ To allow or block requests based on the country that they originate from, create geo match conditions\. For more information, see [Working with geographic match conditions](classic-web-acl-geo-conditions.md)\.
+ To allow or block requests based on whether the requests exceed a specified length, create size constraint conditions\. For more information, see [Working with size constraint conditions](classic-web-acl-size-conditions.md)\.
+ To allow or block requests based on whether the requests appear to contain malicious SQL code, create SQL injection match conditions\. For more information, see [Working with SQL injection match conditions](classic-web-acl-sql-conditions.md)\.
+ To allow or block requests based on strings that appear in the requests, create string match conditions\. For more information, see [Working with string match conditions](classic-web-acl-string-conditions.md)\.
+ To allow or block requests based on a regex pattern that appear in the requests, create regex match conditions\. For more information, see [Working with regex match conditions](classic-web-acl-regex-conditions.md)\.

**Topics**
+ [Working with cross\-site scripting match conditions](classic-web-acl-xss-conditions.md)
+ [Working with IP match conditions](classic-web-acl-ip-conditions.md)
+ [Working with geographic match conditions](classic-web-acl-geo-conditions.md)
+ [Working with size constraint conditions](classic-web-acl-size-conditions.md)
+ [Working with SQL injection match conditions](classic-web-acl-sql-conditions.md)
+ [Working with string match conditions](classic-web-acl-string-conditions.md)
+ [Working with regex match conditions](classic-web-acl-regex-conditions.md)