# Request component options<a name="waf-rule-statement-fields-list"></a>

This section describes the components of the web request that you can specify for inspection\. You specify the request component for match rule statements that look for patterns inside the web request\. These types of statements include string match, regex match, size constraint, and SQL injection attack statements\. For information on how to use these request component settings, see the individual rule statements\. For more information about the rule statements, see [Rule statements list](waf-rule-statements-list.md)

Unless otherwise noted, if a web request doesn't contain the request component that's specified in the rule statement, the request results as not matching the rule\.

**Note**  
You specify a single request component for each rule statement that requires it\. To inspect more than one component of a request, create a rule statement for each component\. 

The AWS WAF console and API documentation provide guidance for the request component settings in the following locations: 
+ **Rule builder** on the console – In the **Statement** settings for a regular rule type, choose the component that you want to inspect in the **Inspect** dialogue under **Request components**\.
+ **API statement contents** – `FieldToMatch`

The rest of this section describes the options for the part of the web request to inspect\. 



## Single header<a name="waf-rule-statement-request-component-single-header"></a>

Inspects a single named header in the request\. For this option, you specify the header key in the **Header field name**, for example, `User-Agent` or `Referer`\. 

## All headers<a name="waf-rule-statement-request-component-headers"></a>

Inspects all of the request headers, including cookies\. You can apply a filter to inspect a subset of all headers\. For this option, you provide the following specifications: 
+ **Match patterns** – The filter to use to obtain a subset of headers for inspection\. AWS WAF looks for these patterns in the headers keys\. 

  The match patterns setting can be one of the following: 
  + **All** – Match all keys\. Evaluate the rule inspection criteria for all headers\. 
  + **Excluded headers** – Inspect only the headers whose keys don't match any of the strings that you specify here\. The string match for a key is case sensitive and must be exact\. 
  + **Included headers** – Inspect only the headers that have a key that matches one of the strings that you specify here\. The string match for a key is case sensitive and must be exact\. 
+ **Match scope** – The parts of the headers that AWS WAF should inspect with the rule inspection criteria\. You can specify **Keys**, **Values**, or **All** for both keys and values\. 
+ **Oversize handling** – How AWS WAF should handle requests that have header data that is larger than AWS WAF can inspect\. You can inspect at most the first 8 KB \(8,192 bytes\) of the request headers and at most the first 200 headers\. The content is available for inspection by AWS WAF up to the first limit reached\. You can choose to continue the inspection, or to skip inspection and mark the request as matching or not matching the rule\. For more information about handling oversize content, see [Oversize handling for request components](waf-rule-statement-oversize-handling.md)\.

## Cookies<a name="waf-rule-statement-request-component-cookies"></a>

Inspects all of the request cookies\. You can apply a filter to inspect a subset of all cookies\. For this option, you provide the following specifications: 
+ **Match patterns** – The filter to use to obtain a subset of cookies for inspection\. AWS WAF looks for these patterns in the cookie keys\. 

  The match patterns setting can be one of the following: 
  + **All** – Match all keys\. Evaluate the rule inspection criteria for all cookies\. 
  + **Excluded cookies** – Inspect only the cookies whose keys don't match any of the strings that you specify here\. The string match for a key is case sensitive and must be exact\. 
  + **Included cookies** – Inspect only the cookies that have a key that matches one of the strings that you specify here\. The string match for a key is case sensitive and must be exact\. 
+ **Match scope** – The parts of the cookies that AWS WAF should inspect with the rule inspection criteria\. You can specify **Keys**, **Values**, or **All** for both keys and values\. 
+ **Oversize handling** – How AWS WAF should handle requests that have cookie data that is larger than AWS WAF can inspect\. You can inspect at most the first 8 KB \(8,192 bytes\) of the request cookies and at most the first 200 cookies\. The content is available for inspection by AWS WAF up to the first limit reached\. You can choose to continue the inspection, or to skip inspection and mark the request as matching or not matching the rule\. For more information about handling oversize content, see [Oversize handling for request components](waf-rule-statement-oversize-handling.md)\.

## Single query parameter<a name="waf-rule-statement-request-component-single-query-param"></a>

Inspects a single query parameter that you have defined as part of the query string\. AWS WAF inspects the value of the parameter that you specify\. 

For this option, you also specify a **Query argument**\. For example, if the URL is `www.xyz.com?UserName=abc&SalesRegion=seattle`, you can specify `UserName` or `SalesRegion` for the query argument\. The maximum length for the name of the argument is 30 characters\. The name is not case sensitive, so if you specify `UserName`, AWS WAF matches all variations of `UserName`, including `username` and `UsERName`\.

If the query string contains more than one instance of the query argument that you've specified, AWS WAF inspects all the values for a match, using `OR` logic\. For example, in the URL `www.xyz.com?SalesRegion=boston&SalesRegion=seattle`, AWS WAF evaluates the name that you've specified against `boston` and `seattle`\. If either is a match, the inspection is a match\.

## All query parameters<a name="waf-rule-statement-request-component-all-query-params"></a>

Inspects all query parameters in the request\. This is similar to the single query parameter component choice, but AWS WAF inspects the values of all arguments within the query string\. For example, if the URL is `www.xyz.com?UserName=abc&SalesRegion=seattle`, AWS WAF triggers a match if either the value of `UserName` or `SalesRegion` match the inspection criteria\. 

Choosing this option adds 10 WCUs to the base cost\.

## URI path<a name="waf-rule-statement-request-component-uri-path"></a>

Inspects the part of a URL that identifies a resource, for example, `/images/daily-ad.jpg`\. For information, see [Uniform Resource Identifier \(URI\): Generic Syntax](https://tools.ietf.org/html/rfc3986#section-3)\. 

If you don't use a text transformation with this option, AWS WAF doesn't normalize the URI and inspects it just as it receives it from the client in the request\. For information about text transformations, see [Text transformations](waf-rule-statement-transformation.md)\.

## Query string<a name="waf-rule-statement-request-component-query-string"></a>

Inspects the part of the URL that appears after a `?` character, if any\.

**Note**  
For cross\-site scripting match statements, we recommend that you choose **All query parameters** instead of **Query string**\. Choosing **All query parameters** adds 10 WCUs to the base cost\.

## Body<a name="waf-rule-statement-request-component-body"></a>

Inspects the request body, evaluated as plain text\. You can also evaluate the body as JSON using the `JSON` content type\. 

The request body is the part of the request that immediately follows the request headers\. It contains any additional data that is needed for the web request, for example, data from a form\. 
+ In the console, you select this under the **Request option** choice **Body**, by selecting the **Content type** choice **Plain text**\. 
+ In the API, in the rule's `FieldToMatch` specification, you specify `Body` to inspect the request body as plain text\.

You must specify oversize handling for this component type\. You can inspect the first 8 KB \(8,192 bytes\) of the body of a request\. Oversize handling defines how AWS WAF handles requests that have body data that is larger than AWS WAF can inspect\. You can choose to continue the inspection, or to skip inspection and mark the request as matching or not matching the rule\. For more information about handling oversize content, see [Oversize handling for request components](waf-rule-statement-oversize-handling.md)\.

You can also evaluate the body as parsed JSON\. For information about this, see the section that follows\. 

## JSON body<a name="waf-rule-statement-request-component-json-body"></a>

Inspects the request body, evaluated as JSON\. You can also evaluate the body as plain text\. 

The request body is the part of the request that immediately follows the request headers\. It contains any additional data that is needed for the web request, for example, data from a form\. 
+ In the console, you select this under the **Request option** choice **Body**, by selecting the **Content type** choice **JSON**\. 
+ In the API, in the rule's `FieldToMatch` specification, you specify `JsonBody`\.

You must specify oversize handling for this component type\. You can inspect the first 8 KB \(8,192 bytes\) of the body of a request\. Oversize handling defines how AWS WAF handles requests that have body data that is larger than AWS WAF can inspect\. You can choose to continue the inspection, or to skip inspection and mark the request as matching or not matching the rule\. For more information about handling oversize content, see [Oversize handling for request components](waf-rule-statement-oversize-handling.md)\.

When AWS WAF inspects the web request body as parsed JSON, it parses and extracts the elements from the JSON and inspects the parts that you indicate using the rule's match statement criteria\. 

Choosing this option doubles the match statement's base cost WCUs\. For example, if the match statement base cost is 5 WCUs without JSON parsing, using JSON parsing doubles the cost to 10 WCUs\. 

With this option, AWS WAF runs two match patterns against the web request body\. The output of the first match pattern is used as input to the second match pattern: 

1. AWS WAF parses and extracts the JSON content and identifies the elements to inspect\. To do this, AWS WAF uses the criteria that you provide in the rule's JSON body specification\.

1. AWS WAF applies any text transformations to the extracted elements and then matches the resulting JSON element set against the rule statement's match criteria\. If any of the elements match, the web request is a match for the rule\. 

You specify the following criteria for AWS WAF to use for the first pattern matching step, to identify the JSON elements to inspect: 
+ **Body parsing fallback behavior** – What AWS WAF should do if it fails to completely parse the JSON body\. The options are the following:
  + **None \(default behavior\)** \- AWS WAF evaluates the content only up to the point where it encountered a parsing error\. 
  + **Evaluate as string** \- Inspect the body as plain text\. AWS WAF applies the text transformations and inspection criteria that you defined for the JSON inspection to the body text string\.
  + **Match** \- Treat the web request as matching the rule statement\. AWS WAF applies the rule action to the request\.
  + **No match** \- Treat the web request as not matching the rule statement\.

  AWS WAF does its best to parse the entire JSON body, but might be forced to stop for reasons such as invalid characters, duplicate keys, truncation, and any content whose root node isn't an object or an array\. 

  AWS WAF parses the JSON in the following examples as two valid key:value pairs: 
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

## HTTP method<a name="waf-rule-statement-request-component-http-method"></a>

Inspects the HTTP method for the request\. The HTTP method indicates the type of operation that the web request is asking your protected resource to perform\. 