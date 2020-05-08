# Working with string match conditions<a name="classic-web-acl-string-conditions"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

If you want to allow or block web requests based on strings that appear in the requests, create one or more string match conditions\. A string match condition identifies the string that you want to search for and the part of web requests, such as a specified header or the query string, that you want AWS WAF Classic to inspect for the string\. Later in the process, when you create a web ACL, you specify whether to allow or block requests that contain the string\.

**Topics**
+ [Creating a string match condition](#classic-web-acl-string-conditions-creating)
+ [Values that you specify when you create or edit string match conditions](#classic-web-acl-string-conditions-values)
+ [Adding and deleting filters in a string match condition](#classic-web-acl-string-conditions-editing)
+ [Deleting string match conditions](#classic-web-acl-string-conditions-deleting)

## Creating a string match condition<a name="classic-web-acl-string-conditions-creating"></a>

When you create string match conditions, you specify filters that identify the string that you want to search for and the part of web requests that you want AWS WAF Classic to inspect for that string, such as the URI or the query string\. You can add more than one filter to a string match condition, or you can create a separate string match condition for each filter\. Here's how each configuration affects AWS WAF Classic behavior:
+ **One filter per string match condition** – When you add the separate string match conditions to a rule and add the rule to a web ACL, web requests must match all the conditions for AWS WAF Classic to allow or block requests based on the conditions\. 

  For example, suppose you create two conditions\. One matches web requests that contain the value `BadBot` in the `User-Agent` header\. The other matches web requests that contain the value `BadParameter` in query strings\. When you add both conditions to the same rule and add the rule to a web ACL, AWS WAF Classic allows or blocks requests only when they contain both values\.
+ **More than one filter per string match condition** – When you add a string match condition that contains multiple filters to a rule and add the rule to a web ACL, a web request needs only to match one of the filters in the string match condition for AWS WAF Classic to allow or block the request based on the one condition\.

  Suppose you create one condition instead of two, and the one condition contains the same two filters as in the preceding example\. AWS WAF Classic allows or blocks requests if they contain *either* `BadBot` in the `User-Agent` header *or* `BadParameter` in the query string\.

**Note**  
When you add a string match condition to a rule, you also can configure AWS WAF Classic to allow or block web requests that *do not* match the values in the condition\.<a name="classic-web-acl-string-conditions-creating-procedure"></a>

**To create a string match condition**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **String and regex matching**\.

1. Choose **Create condition**\.

1. Specify the applicable filter settings\. For more information, see [Values that you specify when you create or edit string match conditions](#classic-web-acl-string-conditions-values)\.

1. Choose **Add filter**\.

1. If you want to add another filter, repeat steps 4 and 5\.

1. When you're finished adding filters, choose **Create**\.

## Values that you specify when you create or edit string match conditions<a name="classic-web-acl-string-conditions-values"></a>

When you create or update a string match condition, you specify the following values: 

**Name**  
Enter a name for the string match condition\. The name can contain only alphanumeric characters \(A\-Z, a\-z, 0\-9\) or the following special characters: \_\-\!"\#`\+\*\},\./\. You can't change the name of a condition after you create it\.

**Type**  
Choose **String match**\.

**Part of the request to filter on**  
Choose the part of each web request that you want AWS WAF Classic to inspect for the string that you specify in **Value to match**:    
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
If duplicate parameters appear in the query string, the values are evaluated as an "OR\." That is, either value will trigger a match\. For example, in the URL "www\.xyz\.com?SalesRegion=boston&SalesRegion=seattle", either "boston" or "seattle" in **Value to match** will trigger a match\.  
If you choose **Single query parameter \(value only\)** you will also specify a **Query parameter name**\. This is the parameter in the query string that you will inspect, such as *UserName* or *SalesRegion*\. The maximum length for **Query parameter name** is 30 characters\. **Query parameter name** is not case sensitive\. For example, it you specify *UserName* as the **Query parameter name**, this will match all variations of *UserName*, such as *username* and *UsERName*\.  
**All query parameters \(values only\)**  
Similar to **Single query parameter \(value only\)**, but rather than inspecting the value of a single parameter, AWS WAF Classic inspects the value of all parameters within the query string for the **Value to match**\. For example, if the URL is "www\.xyz\.com?UserName=abc&SalesRegion=seattle," and you choose **All query parameters \(values only\)**, AWS WAF Classic will trigger a match if the value of either *UserName* or *SalesRegion* is specified as the **Value to match**\. 

**Header \(Only When "Part of the request to filter on" is "Header"\)**  
If you chose **Header** from the **Part of the request to filter on** list, choose a header from the list of common headers, or enter the name of a header that you want AWS WAF Classic to inspect\.

**Match type**  
Within the part of the request that you want AWS WAF Classic to inspect, choose where the string in **Value to match** must appear to match this filter:    
**Contains**  
The string appears anywhere in the specified part of the request\.   
**Contains word**  
The specified part of the web request must include **Value to match**, and **Value to match** must contain only alphanumeric characters or underscore \(A\-Z, a\-z, 0\-9, or \_\)\. In addition, **Value to match** must be a word, which means one of the following:   
+ **Value to match** exactly matches the value of the specified part of the web request, such as the value of a header\.
+ **Value to match** is at the beginning of the specified part of the web request and is followed by a character other than an alphanumeric character or underscore \(\_\), for example, `BadBot;`\.
+ **Value to match** is at the end of the specified part of the web request and is preceded by a character other than an alphanumeric character or underscore \(\_\), for example, `;BadBot`\.
+ **Value to match** is in the middle of the specified part of the web request and is preceded and followed by characters other than alphanumeric characters or underscore \(\_\), for example, `-BadBot;`\.  
**Exactly matches**  
The string and the value of the specified part of the request are identical\.  
**Starts with**  
The string appears at the beginning of the specified part of the request\.   
**Ends with**  
The string appears at the end of the specified part of the request\. 

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

**Value is base64 encoded**  
If the value in **Value to match** is base64\-encoded, select this check box\. Use base64\-encoding to specify non\-printable characters, such as tabs and linefeeds, that attackers include in their requests\.

**Value to match**  
Specify the value that you want AWS WAF Classic to search for in web requests\. The maximum length is 50 bytes\. If you're base64\-encoding the value, the 50\-byte maximum length applies to the value before you encode it\.

## Adding and deleting filters in a string match condition<a name="classic-web-acl-string-conditions-editing"></a>

You can add filters to a string match condition or delete filters\. To change a filter, add a new one and delete the old one\.<a name="classic-web-acl-string-conditions-editing-procedure"></a>

**To add or delete filters in a string match condition**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **String and regex matching**\.

1. Choose the condition that you want to add or delete filters in\.

1. To add filters, perform the following steps:

   1. Choose **Add filter**\.

   1. Specify the applicable filter settings\. For more information, see [Values that you specify when you create or edit string match conditions](#classic-web-acl-string-conditions-values)\.

   1. Choose **Add**\.

1. To delete filters, perform the following steps:

   1. Select the filter that you want to delete\.

   1. Choose **Delete Filter**\.

## Deleting string match conditions<a name="classic-web-acl-string-conditions-deleting"></a>

If you want to delete a string match condition, you need to first delete all filters in the condition and remove the condition from all the rules that are using it, as described in the following procedure\.<a name="classic-web-acl-string-conditions-deleting-procedure"></a>

**To delete a string match condition**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. Remove the string match condition from the rules that are using it:

   1. In the navigation pane, choose **Rules**\.

   1. Choose the name of a rule that is using the string match condition that you want to delete\.

   1. In the right pane, choose **Edit rule**\.

   1. Choose the **X** next to the condition you want to delete\.

   1. Choose **Update**\.

   1. Repeat for all the remaining rules that are using the string match condition that you want to delete\.

1. Remove the filters from the condition you want to delete:

   1. In the navigation pane, choose **String and regex matching**\.

   1. Choose the name of the string match condition that you want to delete\.

   1. In the right pane, choose the check box next to **Filter** in order to select all of the filters\.

   1. Choose the **Delete filter**\.

1. In the navigation pane, choose **String and regex matching**\.

1. In the **String and regex match conditions** pane, choose the string match condition that you want to delete\.

1. Choose **Delete** to delete the selected condition\.