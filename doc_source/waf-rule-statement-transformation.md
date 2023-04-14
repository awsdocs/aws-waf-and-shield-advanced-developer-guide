# Text transformations<a name="waf-rule-statement-transformation"></a>

In statements that look for patterns or set constraints, you can provide transformations for AWS WAF to apply before inspecting the request\. A transformation reformats a web request to eliminate some of the unusual formatting that attackers use in an effort to bypass AWS WAF\. 

When you use this with the JSON body request component selection, AWS WAF applies your transformations after parsing and extracting the elements to inspect from the JSON\. For more information, see the prior section, [JSON body](waf-rule-statement-fields-list.md#waf-rule-statement-request-component-json-body)\.

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
AWS WAF decodes characters that were encoded using CSS 2\.x escape rules `syndata.html#characters`\. This function uses up to two bytes in the decoding process, so it can help to uncover ASCII characters that were encoded using CSS encoding that wouldn’t typically be encoded\. It's also useful in countering evasion, which is a combination of a backslash and non\-hexadecimal characters\. For example, `ja\vascript` for `javascript`\.

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
AWS WAF replaces each occurrence of a C\-style comment \(/\* \.\.\. \*/\) with a single space\. It doesn't compress multiple consecutive occurrences\. It replaces unterminated comments with a space \(ASCII 0x20\)\. It doesn't change a standalone termination of a comment \(\*/\)\.

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