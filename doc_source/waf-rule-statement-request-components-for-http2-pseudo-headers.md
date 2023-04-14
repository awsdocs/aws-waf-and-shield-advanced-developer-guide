# How to inspect HTTP/2 pseudo headers<a name="waf-rule-statement-request-components-for-http2-pseudo-headers"></a>

Protected AWS resources that support HTTP/2 traffic do not forward HTTP/2 pseudo headers to AWS WAF for inspection, but they provide contents of pseudo headers in web request components that AWS WAF inspects\. You can use AWS WAF to inspect only the pseudo headers that are listed in the following table\. 


**HTTP/2 pseudo header contents mapped to web request components**  

| HTTP/2 pseudo header | Web request component to inspect | Documentation | 
| --- | --- | --- | 
|  `:method`  |  HTTP method   |  [HTTP method](waf-rule-statement-fields-list.md#waf-rule-statement-request-component-http-method)  | 
|  `:authority`  |  `Host` header   |  [Single header](waf-rule-statement-fields-list.md#waf-rule-statement-request-component-single-header)  [All headers](waf-rule-statement-fields-list.md#waf-rule-statement-request-component-headers)  | 
|  `:path` URI path  | URI path  | [URI path](waf-rule-statement-fields-list.md#waf-rule-statement-request-component-uri-path) | 
|  `:path` query  |  Query string  |  [Query string](waf-rule-statement-fields-list.md#waf-rule-statement-request-component-query-string) [Single query parameter](waf-rule-statement-fields-list.md#waf-rule-statement-request-component-single-query-param) [All query parameters](waf-rule-statement-fields-list.md#waf-rule-statement-request-component-all-query-params)  | 