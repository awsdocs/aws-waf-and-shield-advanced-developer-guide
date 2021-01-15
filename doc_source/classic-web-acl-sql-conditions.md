# Working with SQL injection match conditions<a name="classic-web-acl-sql-conditions"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

Attackers sometimes insert malicious SQL code into web requests in an effort to extract data from your database\. To allow or block web requests that appear to contain malicious SQL code, create one or more SQL injection match conditions\. A SQL injection match condition identifies the part of web requests, such as the URI path or the query string, that you want AWS WAF Classic to inspect\. Later in the process, when you create a web ACL, you specify whether to allow or block requests that appear to contain malicious SQL code\.

**Topics**
+ [Creating SQL injection match conditions](#classic-web-acl-sql-conditions-creating)
+ [Values that you specify when you create or edit SQL injection match conditions](#classic-web-acl-sql-conditions-values)
+ [Adding and deleting filters in a SQL injection match condition](#classic-web-acl-sql-conditions-editing)
+ [Deleting SQL injection match conditions](#classic-web-acl-sql-conditions-deleting)

## Creating SQL injection match conditions<a name="classic-web-acl-sql-conditions-creating"></a>

When you create SQL injection match conditions, you specify filters, which indicate the part of web requests that you want AWS WAF Classic to inspect for malicious SQL code, such as the URI or the query string\. You can add more than one filter to a SQL injection match condition, or you can create a separate condition for each filter\. Here's how each configuration affects AWS WAF Classic behavior:
+ **More than one filter per SQL injection match condition \(recommended\)** – When you add a SQL injection match condition containing multiple filters to a rule and add the rule to a web ACL, a web request needs only to match one of the filters in the SQL injection match condition for AWS WAF Classic to allow or block the request based on that condition\.

  For example, suppose you create one SQL injection match condition, and the condition contains two filters\. One filter instructs AWS WAF Classic to inspect the URI for malicious SQL code, and the other instructs AWS WAF Classic to inspect the query string\. AWS WAF Classic allows or blocks requests if they appear to contain malicious SQL code *either* in the URI *or* in the query string\.
+ **One filter per SQL injection match condition** – When you add the separate SQL injection match conditions to a rule and add the rule to a web ACL, web requests must match all the conditions for AWS WAF Classic to allow or block requests based on the conditions\. 

  Suppose you create two conditions, and each condition contains one of the two filters in the preceding example\. When you add both conditions to the same rule and add the rule to a web ACL, AWS WAF Classic allows or blocks requests only when both the URI and the query string appear to contain malicious SQL code\.

**Note**  
When you add a SQL injection match condition to a rule, you also can configure AWS WAF Classic to allow or block web requests that *do not* appear to contain malicious SQL code\.<a name="classic-web-acl-sql-conditions-creating-procedure"></a>

**To create a SQL injection match condition**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **SQL injection**\.

1. Choose **Create condition**\.

1. Specify the applicable filter settings\. For more information, see [Values that you specify when you create or edit SQL injection match conditions](#classic-web-acl-sql-conditions-values)\.

1. Choose **Add another filter**\.

1. If you want to add another filter, repeat steps 4 and 5\.

1. When you're finished adding filters, choose **Create**\.

## Values that you specify when you create or edit SQL injection match conditions<a name="classic-web-acl-sql-conditions-values"></a>

When you create or update a SQL injection match condition, you specify the following values: 

**Name**  
The name of the SQL injection match condition\.  
The name can contain only alphanumeric characters \(A\-Z, a\-z, 0\-9\) or the following special characters: \_\-\!"\#`\+\*\},\./\. You can't change the name of a condition after you create it\.

**Part of the request to filter on**  
Choose the part of each web request that you want AWS WAF Classic to inspect for malicious SQL code:    
**Header**  
A specified request header, for example, the `User-Agent` or `Referer` header\. If you choose **Header**, specify the name of the header in the **Header** field\.  
**HTTP method**  
The HTTP method, which indicates the type of operation that the request is asking the origin to perform\. CloudFront supports the following methods: `DELETE`, `GET`, `HEAD`, `OPTIONS`, `PATCH`, `POST`, and `PUT`\.  
**Query string**  
The part of a URL that appears after a `?` character, if any\.  
For SQL injection match conditions, we recommend that you choose **All query parameters \(values only\)** instead of **Query string** for **Part of the request to filter on**\.  
**URI**  
The URI path of the request, which identifies the resource, for example, `/images/daily-ad.jpg`\. This doesn't include the query string or fragment components of the URI\. For information, see [Uniform Resource Identifier \(URI\): Generic Syntax](https://tools.ietf.org/html/rfc3986#section-3.3)\.   
Unless a **Transformation** is specified, a URI is not normalized and is inspected just as AWS receives it from the client as part of the request\. A **Transformation** will reformat the URI as specified\.  
**Body**  
The part of a request that contains any additional data that you want to send to your web server as the HTTP request body, such as data from a form\.  
If you choose **Body** for the value of **Part of the request to filter on**, AWS WAF Classic inspects only the first 8192 bytes \(8 KB\)\. To allow or block requests for which the body is longer than 8192 bytes, you can create a size constraint condition\. \(AWS WAF Classic gets the length of the body from the request headers\.\) For more information, see [Working with size constraint conditions](classic-web-acl-size-conditions.md)\.  
**Single query parameter \(value only\)**  
Any parameter that you have defined as part of the query string\. For example, if the URL is "www\.xyz\.com?UserName=abc&SalesRegion=seattle" you can add a filter to either the *UserName* or *SalesRegion* parameter\.   
If you choose **Single query parameter \(value only\)** you will also specify a **Query parameter name**\. This is the parameter in the query string that you will inspect, such as *UserName* or *SalesRegion*\. The maximum length for **Query parameter name** is 30 characters\. **Query parameter name** is not case sensitive\. For example, it you specify *UserName* as the **Query parameter name**, this will match all variations of *UserName*, such as *username* and *UsERName*\.  
**All query parameters \(values only\)**  
Similar to **Single query parameter \(value only\)**, but rather than inspecting the value of a single parameter, AWS WAF Classic inspects the value of all parameters within the query string for possible malicious SQL code\. For example, if the URL is "www\.xyz\.com?UserName=abc&SalesRegion=seattle," and you choose **All query parameters \(values only\)**, AWS WAF Classic will trigger a match if the value of either *UserName* or *SalesRegion* contain possible malicious SQL code\. 

**Header**  
If you chose **Header** for **Part of the request to filter on**, choose a header from the list of common headers, or enter the name of a header that you want AWS WAF Classic to inspect for malicious SQL code\.

**Transformation**  
A transformation reformats a web request before AWS WAF Classic inspects the request\. This eliminates some of the unusual formatting that attackers use in web requests in an effort to bypass AWS WAF Classic\.   
You can only specify a single type of text transformation\.  
Transformations can perform the following operations:    
**None**  
AWS WAF Classic doesn't perform any text transformations on the web request before inspecting it for the string in **Value to match**\.  
**Convert to lowercase**  
AWS WAF Classic converts uppercase letters \(A\-Z\) to lowercase \(a\-z\)\.  
**HTML decode**  
AWS WAF Classic replaces HTML\-encoded characters with unencoded characters:  
+ Replaces `&quot;` with `&`
+ Replaces `&nbsp;` with a non\-breaking space
+ Replaces `&lt;` with `<`
+ Replaces `&gt;` with `>`
+ Replaces characters that are represented in hexadecimal format, `&#xhhhh;`, with the corresponding characters
+ Replaces characters that are represented in decimal format, `&#nnnn;`, with the corresponding characters  
**Normalize white space**  
AWS WAF Classic replaces the following characters with a space character \(decimal 32\):  
+ \\f, formfeed, decimal 12
+ \\t, tab, decimal 9
+ \\n, newline, decimal 10
+ \\r, carriage return, decimal 13
+ \\v, vertical tab, decimal 11
+ non\-breaking space, decimal 160
In addition, this option replaces multiple spaces with one space\.  
**Simplify command line**  
For requests that contain operating system command line commands, use this option to perform the following transformations:  
+ Delete the following characters: \\ " ' ^
+ Delete spaces before the following characters: / \(
+ Replace the following characters with a space: , ;
+ Replace multiple spaces with one space
+ Convert uppercase letters \(A\-Z\) to lowercase \(a\-z\)  
**URL decode**  
Decode a URL\-encoded request\.

## Adding and deleting filters in a SQL injection match condition<a name="classic-web-acl-sql-conditions-editing"></a>

You can add or delete filters in a SQL injection match condition\. To change a filter, add a new one and delete the old one\.<a name="classic-web-acl-sql-conditions-editing-procedure"></a>

**To add or delete filters in a SQL injection match condition**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **SQL injection**\.

1. Choose the condition that you want to add or delete filters in\.

1. To add filters, perform the following steps:

   1. Choose **Add filter**\.

   1. Specify the applicable filter settings\. For more information, see [Values that you specify when you create or edit SQL injection match conditions](#classic-web-acl-sql-conditions-values)\.

   1. Choose **Add**\.

1. To delete filters, perform the following steps:

   1. Select the filter that you want to delete\.

   1. Choose **Delete filter**\.

## Deleting SQL injection match conditions<a name="classic-web-acl-sql-conditions-deleting"></a>

If you want to delete a SQL injection match condition, you need to first delete all filters in the condition and remove the condition from all the rules that are using it, as described in the following procedure\.<a name="classic-web-acl-sql-conditions-deleting-procedure"></a>

**To delete a SQL injection match condition**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **SQL injection**\.

1. In the **SQL injection match conditions** pane, choose the SQL injection match condition that you want to delete\.

1. In the right pane, choose the **Associated rules** tab\.

   If the list of rules using this SQL injection match condition is empty, go to step 6\. If the list contains any rules, make note of the rules, and continue with step 5\.

1. To remove the SQL injection match condition from the rules that are using it, perform the following steps:

   1. In the navigation pane, choose **Rules**\.

   1. Choose the name of a rule that is using the SQL injection match condition that you want to delete\.

   1. In the right pane, select the SQL injection match condition that you want to remove from the rule, and choose **Remove selected condition**\.

   1. Repeat steps b and c for all of the remaining rules that are using the SQL injection match condition that you want to delete\.

   1. In the navigation pane, choose **SQL injection**\.

   1. In the **SQL injection match conditions** pane, choose the SQL injection match condition that you want to delete\.

1. Choose **Delete** to delete the selected condition\.