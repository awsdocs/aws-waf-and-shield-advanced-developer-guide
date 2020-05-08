# Working with size constraint conditions<a name="classic-web-acl-size-conditions"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

If you want to allow or block web requests based on the length of specified parts of requests, create one or more size constraint conditions\. A size constraint condition identifies the part of web requests that you want AWS WAF Classic to look at, the number of bytes that you want AWS WAF Classic to look for, and an operator, such as greater than \(>\) or less than \(<\)\. For example, you can use a size constraint condition to look for query strings that are longer than 100 bytes\. Later in the process, when you create a web ACL, you specify whether to allow or block requests based on those settings\.

Note that if you configure AWS WAF Classic to inspect the request body, for example, by searching the body for a specified string, AWS WAF Classic inspects only the first 8192 bytes \(8 KB\)\. If the request body for your web requests will never exceed 8192 bytes, you can create a size constraint condition and block requests that have a request body greater than 8192 bytes\.

**Topics**
+ [Creating size constraint conditions](#classic-web-acl-size-conditions-creating)
+ [Values that you specify when you create or edit size constraint conditions](#classic-web-acl-size-conditions-values)
+ [Adding and deleting filters in a size constraint condition](#classic-web-acl-size-conditions-editing)
+ [Deleting size constraint conditions](#classic-web-acl-size-conditions-deleting)

## Creating size constraint conditions<a name="classic-web-acl-size-conditions-creating"></a>

When you create size constraint conditions, you specify filters that identify the part of web requests for which you want AWS WAF Classic to evaluate the length\. You can add more than one filter to a size constraint condition, or you can create a separate condition for each filter\. Here's how each configuration affects AWS WAF Classic behavior:
+ **One filter per size constraint condition** – When you add the separate size constraint conditions to a rule and add the rule to a web ACL, web requests must match all the conditions for AWS WAF Classic to allow or block requests based on the conditions\. 

  For example, suppose you create two conditions\. One matches web requests for which query strings are greater than 100 bytes\. The other matches web requests for which the request body is greater than 1024 bytes\. When you add both conditions to the same rule and add the rule to a web ACL, AWS WAF Classic allows or blocks requests only when both conditions are true\.
+ **More than one filter per size constraint condition** – When you add a size constraint condition that contains multiple filters to a rule and add the rule to a web ACL, a web request needs only to match one of the filters in the size constraint condition for AWS WAF Classic to allow or block the request based on that condition\.

  Suppose you create one condition instead of two, and the one condition contains the same two filters as in the preceding example\. AWS WAF Classic allows or blocks requests if either the query string is greater than 100 bytes or the request body is greater than 1024 bytes\.

**Note**  
When you add a size constraint condition to a rule, you also can configure AWS WAF Classic to allow or block web requests that *do not* match the values in the condition\.<a name="classic-web-acl-size-conditions-creating-procedure"></a>

**To create a size constraint condition**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Size constraints**\.

1. Choose **Create condition**\.

1. Specify the applicable filter settings\. For more information, see [Values that you specify when you create or edit size constraint conditions](#classic-web-acl-size-conditions-values)\.

1. Choose **Add another filter**\.

1. If you want to add another filter, repeat steps 4 and 5\.

1. When you're finished adding filters, choose **Create size constraint condition**\.

## Values that you specify when you create or edit size constraint conditions<a name="classic-web-acl-size-conditions-values"></a>

When you create or update a size constraint condition, you specify the following values: 

**Name**  
Enter a name for the size constraint condition\.  
The name can contain only alphanumeric characters \(A\-Z, a\-z, 0\-9\) or the following special characters: \_\-\!"\#`\+\*\},\./\. You can't change the name of a condition after you create it\.

**Part of the request to filter on**  
Choose the part of each web request for which you want AWS WAF Classic to evaluate the length:    
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
**Single query parameter \(value only\)**  
Any parameter that you have defined as part of the query string\. For example, if the URL is "www\.xyz\.com?UserName=abc&SalesRegion=seattle" you can add a filter to either the *UserName* or *SalesRegion* parameter\.   
If you choose **Single query parameter \(value only\)**, you will also specify a **Query parameter name**\. This is the parameter in the query string that you will inspect, such as *UserName*\. The maximum length for **Query parameter name** is 30 characters\. **Query parameter name** is not case sensitive\. For example, it you specify *UserName* as the **Query parameter name**, this will match all variations of *UserName*, such as *username* and *UsERName*\.  
**All query parameters \(values only\)**  
Similar to **Single query parameter \(value only\)**, but rather than inspecting the value of a single parameter, AWS WAF Classic inspects the values of all parameters within the query string for the size constraint\. For example, if the URL is "www\.xyz\.com?UserName=abc&SalesRegion=seattle," and you choose **All query parameters \(values only\)**, AWS WAF Classic will trigger a match the value of if either *UserName* or *SalesRegion* exceed the specified size\. 

**Header \(Only When "Part of the request to filter on" is "Header"\)**  
If you chose **Header** for **Part of the request to filter on**, choose a header from the list of common headers, or type the name of a header for which you want AWS WAF Classic to evaluate the length\.

**Comparison operator**  
Choose how you want AWS WAF Classic to evaluate the length of the query string in web requests with respect to the value that you specify for **Size**\.  
For example, if you choose **Is greater than** for **Comparison operator** and type **100** for **Size**, AWS WAF Classic evaluates web requests for a query string that is longer than 100 bytes\.

**Size**  
Enter the length, in bytes, that you want AWS WAF Classic to watch for in query strings\.  
If you choose **URI** for the value of **Part of the request to filter on**, the **/** in the URI counts as one character\. For example, the URI `/logo.jpg` is nine characters long\.

**Transformation**  
A transformation reformats a web request before AWS WAF Classic evaluates the length of the specified part of the request\. This eliminates some of the unusual formatting that attackers use in web requests in an effort to bypass AWS WAF Classic\.   
If you choose **Body** for **Part of the request to filter on**, you can't configure AWS WAF Classic to perform a transformation because only the first 8192 bytes are forwarded for inspection\. However, you can still filter your traffic based on the size of the HTTP request body and specify a transformation of **None**\. \(AWS WAF Classic gets the length of the body from the request headers\.\)
You can only specify a single type of text transformation\.  
Transformations can perform the following operations:    
**None**  
AWS WAF Classic doesn't perform any text transformations on the web request before checking the length\.  
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

## Adding and deleting filters in a size constraint condition<a name="classic-web-acl-size-conditions-editing"></a>

You can add or delete filters in a size constraint condition\. To change a filter, add a new one and delete the old one\.<a name="classic-web-acl-size-conditions-editing-procedure"></a>

**To add or delete filters in a size constraint condition**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Size constraint**\.

1. Choose the condition that you want to add or delete filters in\.

1. To add filters, perform the following steps:

   1. Choose **Add filter**\.

   1. Specify the applicable filter settings\. For more information, see [Values that you specify when you create or edit size constraint conditions](#classic-web-acl-size-conditions-values)\.

   1. Choose **Add**\.

1. To delete filters, perform the following steps:

   1. Select the filter that you want to delete\.

   1. Choose **Delete filter**\.

## Deleting size constraint conditions<a name="classic-web-acl-size-conditions-deleting"></a>

If you want to delete a size constraint condition, you need to first delete all filters in the condition and remove the condition from all the rules that are using it, as described in the following procedure\.<a name="classic-web-acl-size-conditions-deleting-procedure"></a>

**To delete a size constraint condition**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Size constraints**\.

1. In the **Size constraint conditions** pane, choose the size constraint condition that you want to delete\.

1. In the right pane, choose the **Associated rules** tab\.

   If the list of rules using this size constraint condition is empty, go to step 6\. If the list contains any rules, make note of the rules, and continue with step 5\.

1. To remove the size constraint condition from the rules that are using it, perform the following steps:

   1. In the navigation pane, choose **Rules**\.

   1. Choose the name of a rule that is using the size constraint condition that you want to delete\.

   1. In the right pane, select the size constraint condition that you want to remove from the rule, and then choose **Remove selected condition**\.

   1. Repeat steps b and c for all the remaining rules that are using the size constraint condition that you want to delete\.

   1. In the navigation pane, choose **Size constraint**\.

   1. In the **Size constraint conditions** pane, choose the size constraint condition that you want to delete\.

1. Choose **Delete** to delete the selected condition\.