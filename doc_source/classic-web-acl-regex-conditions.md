# Working with regex match conditions<a name="classic-web-acl-regex-conditions"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

If you want to allow or block web requests based on strings that match a regular expression \(regex\) pattern that appears in the requests, create one or more regex match conditions\. A regex match condition is a type of string match condition that identifies the pattern that you want to search for and the part of web requests, such as a specified header or the query string, that you want AWS WAF Classic to inspect for the pattern\. Later in the process, when you create a web ACL, you specify whether to allow or block requests that contain the pattern\.

**Topics**
+ [Creating a regex match condition](#classic-web-acl-regex-conditions-creating)
+ [Values that you specify when you create or edit RegEx match conditions](#classic-web-acl-regex-conditions-values)
+ [Editing a regex match condition](#classic-web-acl-regex-conditions-editing)

## Creating a regex match condition<a name="classic-web-acl-regex-conditions-creating"></a>

When you create regex match conditions, you specify pattern sets that identify the string \(using a regular expression\) that you want to search for\. You then add those pattern sets to filters that specify the part of web requests that you want AWS WAF Classic to inspect for that pattern set, such as the URI or the query string\.

You can add multiple regular expressions to a single pattern set\. If you do so, those expressions are combined with an *OR*\. That is, a web request will match the pattern set if the appropriate part of the request matches any of the expressions listed\.

When you add a regex match condition to a rule, you also can configure AWS WAF Classic to allow or block web requests that *do not* match the values in the condition\.

AWS WAF Classic supports most [standard Perl Compatible Regular Expressions \(PCRE\)](http://www.pcre.org/)\. However, the following are not supported:
+ Backreferences and capturing subexpressions
+ Arbitrary zero\-width assertions
+ Subroutine references and recursive patterns
+ Conditional patterns
+ Backtracking control verbs
+ The \\C single\-byte directive
+ The \\R newline match directive
+ The \\K start of match reset directive
+ Callouts and embedded code
+ Atomic grouping and possessive quantifiers<a name="classic-web-acl-regex-conditions-creating-procedure"></a>

**To create a regex match condition**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **String and regex matching**\.

1. Choose **Create condition**\.

1. Specify the applicable filter settings\. For more information, see [Values that you specify when you create or edit RegEx match conditions](#classic-web-acl-regex-conditions-values)\.

1. Choose **Create pattern set and add filter** \(if you created a new pattern set\) or **Add filter** if you used an existing pattern set\.

1. Choose **Create**\.

## Values that you specify when you create or edit RegEx match conditions<a name="classic-web-acl-regex-conditions-values"></a>

When you create or update a regex match condition, you specify the following values: 

**Name**  
Enter a name for the regex match condition\. The name can contain only alphanumeric characters \(A\-Z, a\-z, 0\-9\) or the following special characters: \_\-\!"\#`\+\*\},\./\. You can't change the name of a condition after you create it\.

**Type**  
Choose **Regex match**\.

**Part of the request to filter on**  
Choose the part of each web request that you want AWS WAF Classic to inspect for the pattern that you specify in **Value to match**:    
**Header**  
A specified request header, for example, the `User-Agent` or `Referer` header\. If you choose **Header**, specify the name of the header in the **Header** field\.  
**HTTP method**  
The HTTP method, which indicates the type of operation that the request is asking the origin to perform\. CloudFront supports the following methods: `DELETE`, `GET`, `HEAD`, `OPTIONS`, `PATCH`, `POST`, and `PUT`\.  
**Query string**  
The part of a URL that appears after a `?` character, if any\.  
**URI**  
The part of a URL that identifies a resource, for example, `/images/daily-ad.jpg`\. Unless a **Transformation** is specified, a URI is not normalized and is inspected just as AWS receives it from the client as part of the request\. A **Transformation** will reformat the URI as specified\.  
**Body**  
The part of a request that contains any additional data that you want to send to your web server as the HTTP request body, such as data from a form\.  
If you choose **Body** for the value of **Part of the request to filter on**, AWS WAF Classic inspects only the first 8192 bytes \(8 KB\)\. To allow or block requests for which the body is longer than 8192 bytes, you can create a size constraint condition\. \(AWS WAF Classic gets the length of the body from the request headers\.\) For more information, see [Working with size constraint conditions](classic-web-acl-size-conditions.md)\.  
**Single query parameter \(value only\)**  
Any parameter that you have defined as part of the query string\. For example, if the URL is "www\.xyz\.com?UserName=abc&SalesRegion=seattle" you can add a filter to either the *UserName* or *SalesRegion* parameter\.   
If duplicate parameters appear in the query string, the values are evaluated as an "OR\." That is, either value will trigger a match\. For example, in the URL "www\.xyz\.com?SalesRegion=boston&SalesRegion=seattle", a pattern that matches either "boston" or "seattle" in **Value to match** will trigger a match\.  
If you choose **Single query parameter \(value only\)** you will also specify a **Query parameter name**\. This is the parameter in the query string that you will inspect, such as *UserName* or *SalesRegion*\. The maximum length for **Query parameter name** is 30 characters\. **Query parameter name** is not case sensitive\. For example, it you specify *UserName* as the **Query parameter name**, this will match all variations of *UserName*, such as *username* and *UsERName*\.  
**All query parameters \(values only\)**  
Similar to **Single query parameter \(value only\)**, but rather than inspecting the value of a single parameter, AWS WAF Classic inspects the value of all parameters within the query string for the pattern specified in the **Value to match**\. For example, in the URL "www\.xyz\.com?UserName=abc&SalesRegion=seattle", a pattern in **Value to match** that matches either the value in *UserName* or *SalesRegion* will trigger a match\.

**Header \(Only When "Part of the request to filter on" is "Header"\)**  
If you chose **Header** from the **Part of the request to filter on** list, choose a header from the list of common headers, or enter the name of a header that you want AWS WAF Classic to inspect\.

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
When you're concerned that attackers are injecting an operating system command line command and using unusual formatting to disguise some or all of the command, use this option to perform the following transformations:  
+ Delete the following characters: \\ " ' ^
+ Delete spaces before the following characters: / \(
+ Replace the following characters with a space: , ;
+ Replace multiple spaces with one space
+ Convert uppercase letters \(A\-Z\) to lowercase \(a\-z\)  
**URL decode**  
Decode a URL\-encoded request\.

**Regex pattern to match to request**  
You can choose an existing pattern set, or create a new one\. If you create a new one specify the following:    
New pattern set name  
Enter a name and then specify the regex pattern that you want AWS WAF Classic to search for\.   
If you add multiple regular expressions to a pattern set, those expressions are combined with an *OR*\. That is, a web request will match the pattern set if the appropriate part of the request matches any of the expressions listed\.  
The maximum length of **Value to match** is 70 characters\. 

## Editing a regex match condition<a name="classic-web-acl-regex-conditions-editing"></a>

You can make the following changes to an existing regex match condition:
+ Delete a pattern from an existing pattern set
+ Add a pattern to an existing pattern set
+ Delete a filter to an existing regex match condition
+ Add a filter to an existing regex match condition \(You can have only one filter in a regex match condition\. Therefore, in order to add a filter, you must delete the existing filter first\.\)
+ Delete an existing regex match condition

**Note**  
You cannot add or delete a pattern set from an existing filter\. You must either edit the pattern set, or delete the filter and create a new filter with a new pattern set\.<a name="classic-web-acl-regex-conditions-editing-procedure-delete-pattern"></a>

**To delete a pattern from an existing pattern set**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **String and regex matching**\.

1. Choose **View regex pattern sets**\.

1. Choose the name of the pattern set you want to edit\.

1. Choose **Edit**\.

1. Choose the **X** next to the pattern you want to delete\.

1. Choose **Save**\.<a name="classic-web-acl-regex-conditions-editing-procedure-add-pattern"></a>

**To add a pattern to an existing pattern set**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **String and regex matching**\.

1. Choose **View regex pattern sets**\.

1. Choose the name of the pattern set to edit\.

1. Choose **Edit**\.

1. Enter a new regex pattern\.

1. Choose the **\+** next to the new pattern\.

1. Choose **Save**\.<a name="classic-web-acl-regex-conditions-editing-procedure-delete-filter"></a>

**To delete a filter from an existing regex match condition**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **String and regex matching**\.

1. Choose the name of the condition with the filter you want to delete\.

1. Choose the box next to the filter you want to delete\.

1. Choose **Delete filter**\.<a name="classic-web-acl-regex-conditions-editing-procedure-delete-regex-condition"></a>

**To delete a regex match condition**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. Delete the filter from the regex condition\. See [To delete a filter from an existing regex match condition](#classic-web-acl-regex-conditions-editing-procedure-delete-filter) for instructions to do this\.\)

1. Remove the regex match condition from the rules that are using it:

   1. In the navigation pane, choose **Rules**\.

   1. Choose the name of a rule that is using the regex match condition that you want to delete\.

   1. In the right pane, choose **Edit rule**\.

   1. Choose the **X** next to the condition you want to delete\.

   1. Choose **Update**\.

   1. Repeat for all the remaining rules that are using the regex match condition that you want to delete\.

1. In the navigation pane, choose **String and regex matching**\.

1. Select the button next to the condition you want to delete\.

1. Choose **Delete**\.<a name="classic-web-acl-regex-conditions-editing-procedure-add-filter"></a>

**To add or change a filter to an existing regex match condition**

You can have only one filter in a regex match condition\. If you want to add or change the filter, you must first delete the existing filter\.

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. Delete the filter from the regex condition you want to change\. See [To delete a filter from an existing regex match condition](#classic-web-acl-regex-conditions-editing-procedure-delete-filter) for instructions to do this\.\)

1. In the navigation pane, choose **String and regex matching**\.

1. Choose the name of the condition you want to change\.

1. Choose **Add filter**\.

1. Enter the appropriate values for the new filter and choose **Add**\.