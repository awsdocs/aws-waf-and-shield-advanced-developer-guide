# Working with Cross\-site Scripting Match Conditions<a name="web-acl-xss-conditions"></a>

Attackers sometimes insert scripts into web requests in an effort to exploit vulnerabilities in web applications\. You can create one or more cross\-site scripting match conditions to identify the parts of web requests, such as the URI or the query string, that you want AWS WAF to inspect for possible malicious scripts\. Later in the process, when you create a web ACL, you specify whether to allow or block requests that appear to contain malicious scripts\.


+ [Creating Cross\-site Scripting Match Conditions](#web-acl-xss-conditions-creating)
+ [Values That You Specify When You Create or Edit Cross\-site Scripting Match Conditions](#web-acl-xss-conditions-values)
+ [Adding and Deleting Filters in a Cross\-site Scripting Match Condition](#web-acl-xss-conditions-editing)
+ [Deleting Cross\-site Scripting Match Conditions](#web-acl-xss-conditions-deleting)

## Creating Cross\-site Scripting Match Conditions<a name="web-acl-xss-conditions-creating"></a>

When you create cross\-site scripting match conditions, you specify filters, which indicate the part of web requests that you want AWS WAF to inspect for malicious scripts, such as the URI or the query string\. You can add more than one filter to a cross\-site scripting match condition, or you can create a separate condition for each filter\. Here's how each configuration affects AWS WAF behavior:

+ **More than one filter per cross\-site scripting match condition \(recommended\)** – When you add a cross\-site scripting match condition that contains multiple filters to a rule and add the rule to a web ACL, a web request must match only one of the filters in the cross\-site scripting match condition for AWS WAF to allow or block the request based on that condition\.

  For example, suppose you create one cross\-site scripting match condition, and the condition contains two filters\. One filter instructs AWS WAF to inspect the URI for malicious scripts, and the other instructs AWS WAF to inspect the query string\. AWS WAF allows or blocks requests if they appear to contain malicious scripts *either* in the URI *or* in the query string\.

+ **One filter per cross\-site scripting match condition** – When you add the separate cross\-site scripting match conditions to a rule and add the rule to a web ACL, web requests must match all the conditions for AWS WAF to allow or block requests based on the conditions\. 

  Suppose you create two conditions, and each condition contains one of the two filters in the preceding example\. When you add both conditions to the same rule and add the rule to a web ACL, AWS WAF allows or blocks requests only when both the URI and the query string appear to contain malicious scripts\.

**Note**  
When you add a cross\-site scripting match condition to a rule, you also can configure AWS WAF to allow or block web requests that *do not* appear to contain malicious scripts\.

**To create a cross\-site scripting match condition**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/waf/](https://console.aws.amazon.com/waf/)\. 

1. In the navigation pane, choose **Cross\-site scripting**\.

1. Choose **Create condition**\.

1. Specify the applicable filter settings\. For more information, see [Values That You Specify When You Create or Edit Cross\-site Scripting Match Conditions](#web-acl-xss-conditions-values)\.

1. Choose **Add another filter**\.

1. If you want to add another filter, repeat steps 4 and 5\.

1. When you're done adding filters, choose **Create**\.

## Values That You Specify When You Create or Edit Cross\-site Scripting Match Conditions<a name="web-acl-xss-conditions-values"></a>

When you create or update a cross\-site scripting match condition, you specify the following values: 

**Name**  
The name of the cross\-site scripting match condition\.  
The name can contain only the characters A\-Z, a\-z, and 0\-9\. You can't change the name of a condition after you create it\.

**Part of the request to filter on**  
Choose the part of each web request that you want AWS WAF to inspect for malicious scripts:    
**Header**  
A specified request header, for example, the `User-Agent` or `Referer` header\. If you choose **Header**, specify the name of the header in the **Header** field\.  
**HTTP method**  
The HTTP method, which indicates the type of operation that the request is asking the origin to perform\. CloudFront supports the following methods: `DELETE`, `GET`, `HEAD`, `OPTIONS`, `PATCH`, `POST`, and `PUT`\.  
**Query string**  
The part of a URL that appears after a `?` character, if any\.  
**URI**  
The part of a URL that identifies a resource, for example, `/images/daily-ad.jpg`\.  
**Body**  
The part of a request that contains any additional data that you want to send to your web server as the HTTP request body, such as data from a form\.  
If you choose **Body** for the value of **Part of the request to filter on**, AWS WAF inspects only the first 8192 bytes \(8 KB\)\. To allow or block requests for which the body is longer than 8192 bytes, you can create a size constraint condition\. \(AWS WAF gets the length of the body from the request headers\.\) For more information, see [Working with Size Constraint Conditions](web-acl-size-conditions.md)\.

**Header**  
If you chose **Header** for **Part of the request to filter on**, choose a header from the list of common headers, or type the name of a header that you want AWS WAF to inspect for malicious scripts\.

**Transformation**  
A transformation reformats a web request before AWS WAF inspects the request\. This eliminates some of the unusual formatting that attackers use in web requests in an effort to bypass AWS WAF\. Transformations can perform the following operations:    
**None**  
AWS WAF doesn't perform any text transformations on the web request before inspecting it for the string in **Value to match**\.  
**Convert to lowercase**  
AWS WAF converts uppercase letters \(A\-Z\) to lowercase \(a\-z\)\.  
**HTML decode**  
AWS WAF replaces HTML\-encoded characters with unencoded characters:  

+ Replaces `&quot;` with `&`

+ Replaces `&nbsp;` with a non\-breaking space

+ Replaces `&lt;` with `<`

+ Replaces `&gt;` with `>`

+ Replaces characters that are represented in hexadecimal format, `&#xhhhh;`, with the corresponding characters

+ Replaces characters that are represented in decimal format, `&#nnnn;`, with the corresponding characters  
**Normalize whitespace**  
AWS WAF replaces the following characters with a space character \(decimal 32\):  

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

## Adding and Deleting Filters in a Cross\-site Scripting Match Condition<a name="web-acl-xss-conditions-editing"></a>

You can add or delete filters in a cross\-site scripting match condition\. To change a filter, add a new one and delete the old one\.

**To add or delete filters in a cross\-site scripting match condition**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/waf/](https://console.aws.amazon.com/waf/)\. 

1. In the navigation pane, choose **Cross\-site scripting**\.

1. Choose the condition that you want to add or delete filters in\.

1. To add filters, perform the following steps:

   1. Choose **Add filter**\.

   1. Specify the applicable filter settings\. For more information, see [Values That You Specify When You Create or Edit Cross\-site Scripting Match Conditions](#web-acl-xss-conditions-values)\.

   1. Choose **Add**\.

1. To delete filters, perform the following steps:

   1. Select the filter that you want to delete\.

   1. Choose **Delete filter**\.

## Deleting Cross\-site Scripting Match Conditions<a name="web-acl-xss-conditions-deleting"></a>

If you want to delete a cross\-site scripting match condition, you must first delete all filters in the condition and remove the condition from all the rules that are using it, as described in the following procedure\.

**To delete a cross\-site scripting match condition**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/waf/](https://console.aws.amazon.com/waf/)\. 

1. In the navigation pane, choose **Cross\-site scripting**\.

1. In the **Cross\-site scripting match conditions** pane, choose the cross\-site scripting match condition that you want to delete\.

1. In the right pane, choose the **Associated rules** tab\.

   If the list of rules using this cross\-site scripting match condition is empty, go to step 6\. If the list contains any rules, make note of the rules, and continue with step 5\.

1. To remove the cross\-site scripting match condition from the rules that are using it, perform the following steps:

   1. In the navigation pane, choose **Rules**\.

   1. Choose the name of a rule that is using the cross\-site scripting match condition that you want to delete\.

   1. In the right pane, select the cross\-site scripting match condition that you want to remove from the rule, and choose **Remove selected condition**\.

   1. Repeat steps b and c for all the remaining rules that are using the cross\-site scripting match condition that you want to delete\.

   1. In the navigation pane, choose **Cross\-site scripting**\.

   1. In the **Cross\-site scripting match conditions** pane, choose the cross\-site scripting match condition that you want to delete\.

1. Choose **Delete** to delete the selected condition\.