# Web request component settings<a name="waf-rule-statement-fields"></a>

This section describes the settings that you can specify for rule statements that inspect a component of the web request\. For information on usage, see the individual rule statements\. 

## Request component<a name="waf-rule-statement-request-component"></a>

The request component specifies the part of a web request for AWS WAF to inspect\. You specify this for standard rule statements that look for patterns inside the web request\. These include regex pattern match, SQL injection attack, and size constraint statements\. 

Unless otherwise noted, if a web request doesn't have the request component that's specified in the rule statement, the request results as not matching the rule\.

**Note**  
You specify a single request component for each rule statement that requires it\. To inspect more than one component of a request, create a rule statement for each component\. 

The AWS WAF console and API documentation provide guidance for these settings in the following locations: 
+ **Rule builder** on the console – in the **Statement** settings for a regular rule type, choose the component that you want to inspect in the **Inspect** dialogue under **Request components**\.
+ **API statement contents** – `FieldToMatch`

Here are the options for the part of the web request to inspect: Options for the part of the request to inspect

**Header**  
A specific request header\. For this option, you also choose the name of the header in the **Header type** field, for example, `User-Agent` or `Referer`\. 

**HTTP method**  
The HTTP method, which indicates the type of operation that the web request is asking the origin to perform\. 

**Query string**  
The part of a URL that appears after a `?` character, if any\.  
For cross\-site scripting match conditions, we recommend that you choose **All query parameters** instead of **Query string**\. Choosing **All query parameters** adds 10 WCUs to the base cost\.

**Single query parameter**  
Any parameter that you have defined as part of the query string\. AWS WAF inspects the value of the parameter that you specify\.   
For this option, you also specify a **Query parameter name**\. For example, if the URL is `www.xyz.com?UserName=abc&SalesRegion=seattle`, you can specify `UserName` or `SalesRegion` for the name\. The maximum length for the name is 30 characters\. The name is not case sensitive, so if you specify `UserName` as the name, AWS WAF matches all variations of `UserName`, including `username` and `UsERName`\.  
If the query string contains more than one instance of the name that you've specified, AWS WAF inspects all the values for a match, using `OR` logic\. For example, in the URL `www.xyz.com?SalesRegion=boston&SalesRegion=seattle`, AWS WAF evaluates the name that you've specified against `boston` and `seattle`\. If either is a match, the inspection is a match\.

**All query parameters**  
Similar to **Single query parameter**, but AWS WAF inspects the values of all parameters within the query string\. For example, if the URL is `www.xyz.com?UserName=abc&SalesRegion=seattle`, AWS WAF triggers a match if either the value of `UserName` or `SalesRegion` match the inspection criteria\.   
Choosing this option adds 10 WCUs to the base cost\.

**URI path**  
The part of a URL that identifies a resource, for example, `/images/daily-ad.jpg`\. If you don't use a text transformation with this option, AWS WAF doesn't normalize the URI and inspects it just as it receives it from the client in the request\. 

**Body**  
The part of the request that immediately follows the request headers, evaluated as plain text\. This contains any additional data that is needed for the web request, for example, data from a form\.   
+ In the console, you select this under the **Request option** choice **Body**, by selecting the **Content type** choice **Plain text**\. 
+ In the API, in the rule's `FieldToMatch` specification, you specify `Body` to inspect the request body as plain text\.
Only the first 8 KB \(8,192 bytes\) of the request body are forwarded to AWS WAF for inspection\. For information about how to manage this, see [Web request body inspection](web-request-body-inspection.md)\. 
You can also evaluate the body as parsed JSON\. For information about this, see the sections that follow\. 

**JSON body**  
The part of the request that immediately follows the request headers, evaluated as parsed JSON\. The body contains any additional data that is needed for the web request, for example, data from a form\. You can also evaluate the body as plain text\. For information about this, see the preceding section\.   
+ In the console, you select this under the **Request option** choice **Body**, by selecting the **Content type** choice **JSON**\. 
+ In the API, in the rule's `FieldToMatch` specification, you specify `JsonBody`\.
Only the first 8 KB \(8,192 bytes\) of the request body are forwarded to AWS WAF for inspection\. For information about how to manage this, see [Web request body inspection](web-request-body-inspection.md)\. 
For details about JSON body inspection, see the following section\. Choosing the JSON body option doubles the match statement's base cost WCUs\. For example, if the match statement base cost is 5 WCUs without JSON parsing, using JSON parsing doubles the cost to 10 WCUs\. 

## JSON body request component<a name="waf-rule-statement-request-component-json-body"></a>

JSON body inspection provides a specialized inspection of a web request body\. For general information about web request body inspection, see the prior section\. 

**Warning**  
Only the first 8 KB \(8,192 bytes\) of the request body are forwarded to AWS WAF for inspection\. For information about how to manage this, see [Web request body inspection](web-request-body-inspection.md)\. 

When AWS WAF inspects the web request body as parsed JSON, it parses and extracts the elements from the JSON and inspects the parts that you indicate using the rule's match statement criteria\. 

Choosing this option doubles the match statement's base cost WCUs\. For example, if the match statement base cost is 5 WCUs without JSON parsing, using JSON parsing doubles the cost to 10 WCUs\. 

With this option, AWS WAF runs two match patterns against the web request body, with the output of the first used as input to the second: 

1. AWS WAF parses and extracts the JSON content and identifies the elements to inspect\. To do this, AWS WAF uses the criteria that you provide in the rule's JSON body specification\.

1. AWS WAF applies any text transformations to the extracted elements and then matches the resulting JSON element set against the rule statement's match criteria\. If any of the elements match, the web request is a match for the rule\. 

You specify the following criteria for AWS WAF to use for the first pattern matching step, to identify the JSON elements to inspect: 
+ **Body parsing fallback behavior** – What AWS WAF should do if it fails to completely parse the JSON body\. The options are the following:
  + **None \(default behavior\)** \- AWS WAF evaluates the content only up to the point where it encountered a parsing error\. 
  + **Evaluate as string** \- Inspect the body as plain text\. AWS WAF applies the text transformations and inspection criteria that you defined for the JSON inspection to the body text string\.
  + **Match** \- Treat the web request as matching the rule statement\. AWS WAF applies the rule action to the request\.
  + **No match** \- Treat the web request as not matching the rule statement\.

  AWS WAF does its best to parse the entire JSON body, but might be forced to stop for reasons such as invalid characters, duplicate keys, truncation, and any content whose root node isn't an object or an array\. 

  AWS WAF parses the JSON in the following examples as two valid key, value pairs: 
  + Missing comma: `{"key1":"value1""key2":"value2"}`
  + Missing colon: `{"key1":"value1","key2""value2"}`
  + Extra colons: `{"key1"::"value1","key2""value2"}`
+ **JSON match scope** – The types of elements in the JSON that AWS WAF should inspect\. You can specify **Keys**, **Values**, or **All** for both keys and values\. 
+ **Content to inspect** – The elements in the parsed and extracted JSON that you want AWS WAF to inspect\. 

  You must specify one of the following:
  + **Full JSON content** \- Evaluate all elements in the parsed JSON\. 
  + **Only included elements** \- Evaluate only elements in the JSON that match the JSON Pointer criteria that you provide\. For information about the JSON Pointer syntax, see the Internet Engineering Task Force \(IETF\) documentation [JavaScript Object Notation \(JSON\) Pointer](https://tools.ietf.org/html/rfc6901)\. 

    Don't use this option to include *all* paths in the JSON\. Use **Full JSON content** instead\. 

    For example, in the console, you can provide the following: 

    ```
    /dogs/0/name
    /dogs/1/name
    ```

    In the API or CLI, you can provide the following: 

    ```
    "IncludedPaths": ["/dogs/0/name", "/dogs/1/name"]
    ```

**Example JSON body inspection scenario**  
If the included elements setting is `/a/b`, then for the following JSON body: 

```
{ 
  "a":{
    "c":"d",
    "b":{
      "e":{
        "f":"g"
      }
    }
  }
}
```

The following list describes what AWS WAF would evaluate for each match scope setting\. The key `b`, which is part of the included elements path, isn't evaluated\.
+ For a match scope set to all: `e`, `f,` and `g`\.
+ For a match scope set to keys: `e` and `f`\.
+ For a match scope set to values: `g`\.

## Text transformations<a name="waf-rule-statement-transformation"></a>

In statements that look for patterns or set constraints, you can provide transformations for AWS WAF to apply before inspecting the request\. A transformation reformats a web request to eliminate some of the unusual formatting that attackers use in an effort to bypass AWS WAF\. 

When you use this with the JSON body request component selection, AWS WAF applies your transformations after parsing and extracting the elements to inspect from the JSON\. For more information, see the prior section, [JSON body request component](#waf-rule-statement-request-component-json-body)\.

If you provide more than one transformation, you also set the order for AWS WAF to apply them\. 

**WCUs** – Each text transformation is 10 WCUs\.

The AWS WAF console and API documentation also provide guidance for these settings in the following locations: 
+ **Rule builder** on the console – **Text transformation**\. This option is available when you use request components\. 
+ **API statement contents** – `TextTransformations`Options for text transformations

Base64 decode  
AWS WAF decodes a Base64\-encoded string\.

Base64 decode ext  
AWS WAF decodes a Base64\-encoded string, but uses a forgiving implementation that ignores characters that aren't valid\. 

Command line  
This option mitigates situations where attackers might be injecting an operating system command line command and are using unusual formatting to disguise some or all of the command\.   
Use this option to perform the following transformations:  
+ Delete the following characters: `\ " ' ^`
+ Delete spaces before the following characters: `/ (`
+ Replace the following characters with a space: `, ;`
+ Replace multiple spaces with one space
+ Convert uppercase letters, `A-Z`, to lowercase, `a-z`

Compress white space  
AWS WAF replaces multiple spaces with one space and replaces the following characters with a space character \(decimal 32\):  
+ `\f`, formfeed, decimal 12
+ `\t`, tab, decimal 9
+ `\n`, newline, decimal 10
+ `\r`, carriage return, decimal 13
+ `\v`, vertical tab, decimal 11
+ non\-breaking space, decimal 160

CSS decode  
AWS WAF decodes characters that were encoded using CSS 2\.x escape rules `syndata.html#characters`\. This function uses up to two bytes in the decoding process, so it can help to uncover ASCII characters that were encoded using CSS encoding that wouldn’t typically be encoded\. It's also useful in countering evasion, which is a combination of a backslash and non\-hexadecimal characters\. For example, ja\\vascript for javascript\.

Escape sequence decode  
AWS WAF decodes the following ANSI C escape sequences: `\a, \b, \f, \n, \r, \t, \v, \\, \?, \', \", \xHH (hexadecimal), \0OOO (octal)`\. Encodings that aren't valid remain in the output\.

Hex decode  
AWS WAF decodes a string of hexadecimal characters into a binary\.

HTML entity decode  
AWS WAF replaces HTML\-encoded characters with unencoded characters:  
+ Replaces `&quot;` with `"`
+ Replaces `&nbsp;` with a non\-breaking space, decimal 160
+ Replaces `&lt;` with `<`
+ Replaces `&gt;` with `>`
+ Replaces characters that are represented in hexadecimal format, `&#xhhhh;`, with the corresponding characters
+ Replaces characters that are represented in decimal format, `&#nnnn;`, with the corresponding characters

JS decode  
AWS WAF decodes JavaScript escape sequences\. If a `\uHHHH` code is in the full\-width ASCII code range of `FF01-FF5E`, then the higher byte is used to detect and adjust the lower byte\. If not, only the lower byte is used and the higher byte is zeroed, causing a possible loss of information\.

Lowercase  
AWS WAF converts uppercase letters \(A\-Z\) to lowercase \(a\-z\)\.

MD5  
AWS WAF calculates an MD5 hash from the data in the input\. The computed hash is in a raw binary form\.

None  
AWS WAF inspects the web request as received, without any text transformations\. 

Normalize path  
AWS WAF removes multiple slashes, directory self\-references, and directory back\-references that are not at the beginning of the input from an input string\.

Normalize path win  
AWS WAF processes this like `NORMALIZE_PATH`, but first converts backslash characters to forward slashes\.

Remove nulls  
AWS WAF removes all `NULL` bytes from the input\. 

Replace comments  
AWS WAF replaces each occurrence of a C\-style comment \(/\* \.\.\. \*/\) with a single space\. Multiple consecutive occurrences are not compressed\. Unterminated comments are also replaced with a space \(ASCII 0x20\)\. However, a standalone termination of a comment \(\*/\) is not acted upon\.

Replace nulls  
AWS WAF replaces `NULL` bytes in the input with space characters \(ASCII 0x20\)\.

SQL hex decode  
AWS WAF decodes SQL hex data\. For example, \(`0x414243`\) is decoded to \(`ABC`\)\.

URL decode  
AWS WAF decodes a URL\-encoded value\.

URL decode uni  
Like `URL_DECODE`, but with support for Microsoft\-specific `%u` encoding\. If the code is in the full\-width ASCII code range of `FF01-FF5E`, the higher byte is used to detect and adjust the lower byte\. Otherwise, only the lower byte is used and the higher byte is zeroed\.

UTF8 to Unicode  
AWS WAF converts all UTF\-8 character sequences to Unicode\. This helps input normalization, and minimizes false\-positives and false\-negatives for non\-English languages\.