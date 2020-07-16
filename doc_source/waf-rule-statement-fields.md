# Request component settings<a name="waf-rule-statement-fields"></a>

This section describes the settings that you can specify for rule statements that inspect a component of the web request\. For information on usage, see the individual rule statements\. 

## Request component<a name="waf-rule-statement-request-component"></a>

The request component specifies the part of a web request for AWS WAF to inspect\. You specify this for standard rule statements that look for patterns inside the web request\. These include regex pattern match, SQL injection attack, and size constraint statements\. 

**Note**  
You specify a single request component for each rule statement that requires it\. To inspect more than one component of a request, create a rule statement for each component\. 

The AWS WAF console and API documentation provide guidance for these settings in the following locations: 
+ **Rule builder** on the console – For **Request option**, choose **Request components**\.
+ **API statement contents** – `FieldToMatch`

Here are the options for the part of the web request to inspect: Options for the part of the request to inspect

**Header**  
A specific request header\. For this option, you also choose the name of the header in the **Header type** field, for example, `User-Agent` or `Referer`\. 

**HTTP method**  
The HTTP method, which indicates the type of operation that the web request is asking the origin to perform\. 

**Query string**  
The part of a URL that appears after a `?` character, if any\.  
For cross\-site scripting match conditions, we recommend that you choose **All query parameters** instead of **Query string**\.

**Single query parameter**  
Any parameter that you have defined as part of the query string\. AWS WAF inspects the value of the parameter that you specify\.   
For this option, you also specify a **Query parameter name**\. For example, if the URL is `www.xyz.com?UserName=abc&SalesRegion=seattle`, you can specify `UserName` or `SalesRegion` for the name\. The maximum length for the name is 30 characters\. The name is not case sensitive, so if you specify `UserName` as the name, AWS WAF matches all variations of `UserName`, including `username` and `UsERName`\.  
If the query string contains more than one instance of the name that you've specified, AWS WAF inspects all the values for a match, using OR logic\. For example, in the URL `www.xyz.com?SalesRegion=boston&SalesRegion=seattle`, AWS WAF evaluates the name that you've specified against `boston` and `seattle`\. If either is a match, the inspection is a match\.

**All query parameters**  
Similar to **Single query parameter**, but AWS WAF inspects the values of all parameters within the query string\. For example, if the URL is `www.xyz.com?UserName=abc&SalesRegion=seattle`, AWS WAF triggers a match if either the value of `UserName` or `SalesRegion` match the inspection criteria\. 

**URI**  
The part of a URL that identifies a resource, for example, `/images/daily-ad.jpg`\. If you don't use a text transformation with this option, AWS WAF doesn't normalize the URI and inspects it just as it receives it from the client in the request\. 

**Body**  
The part of the request that immediately follows the request headers\. This contains any additional data that is needed for the web request, for example, data from a form\.  
Only the first 8 KB \(8,192 bytes\) of the request body are forwarded to AWS WAF for inspection\. If you don't need to inspect more than 8 KB, you can guarantee that you don't allow additional bytes in by combining your statement that inspects the body of the web request, such as a string match rule statement, with a size constraint rule statement that enforces an 8 KB max size on the body of the request\. For information about size constraint statements, see [Size constraint rule statement](waf-rule-statement-type-size-constraint-match.md)\. AWS WAF doesn't support inspecting the entire contents of web requests whose bodies exceed 8 KB\. 

## Text transformations<a name="waf-rule-statement-transformation"></a>

In statements that look for patterns or set constraints, you can provide transformations for AWS WAF to apply before inspecting the request\. A transformation reformats a web request to eliminate some of the unusual formatting that attackers use in an effort to bypass AWS WAF\. 

If you provide more than one transformation, you also set the order for AWS WAF to apply them\. 

**WCUs** – Each text transformation is 10 WCUs\.

The AWS WAF console and API documentation also provide guidance for these settings in the following locations: 
+ **Rule builder** on the console – **Text transformation**\. This option is available when you use request components\. 
+ **API statement contents** – `TextTransformations`Options for text transformations

None  
AWS WAF inspects the web request as received\. 

Convert to lowercase  
AWS WAF converts any uppercase letters, `A-Z`, to lowercase, `a-z`\.

HTML decode  
AWS WAF replaces HTML\-encoded characters with unencoded characters:  
+ Replaces `&quot;` with `&`
+ Replaces `&nbsp;` with a non\-breaking space
+ Replaces `&lt;` with `<`
+ Replaces `&gt;` with `>`
+ Replaces characters that are represented in hexadecimal format, `&#xhhhh;`, with the corresponding characters
+ Replaces characters that are represented in decimal format, `&#nnnn;`, with the corresponding characters

Normalize white space  
AWS WAF replaces multiple spaces with one space and replaces the following characters with a space character \(decimal 32\):  
+ `\f`, formfeed, decimal 12
+ `\t`, tab, decimal 9
+ `\n`, newline, decimal 10
+ `\r`, carriage return, decimal 13
+ `\v`, vertical tab, decimal 11
+ non\-breaking space, decimal 160

Simplify command line  
This option mitigates situations where attackers might be injecting an operating system command line command and are using unusual formatting to disguise some or all of the command\.   
Use this option to perform the following transformations:  
+ Delete the following characters: `\ " ' ^`
+ Delete spaces before the following characters: `/ (`
+ Replace the following characters with a space: `, ;`
+ Replace multiple spaces with one space
+ Convert uppercase letters, `A-Z`, to lowercase, `a-z`

URL decode  
Decode a URL\-encoded request\.