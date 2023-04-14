# Web request components<a name="waf-rule-statement-fields"></a>

This section describes the settings that you can specify for rule statements that inspect a component of the web request\. For information on usage, see the individual rule statements\. 

For the request component settings, you need to specify the component type itself, and additional options that depend on the type\. For example, if you choose a component type that contains text to be inspected, you can specify text transformations that you want AWS WAF to apply before evaluating your inspection criteria\. 

Unless otherwise noted, if a web request doesn't have the request component that's specified in the rule statement, the request results as not matching the rule\.

**Contents**
+ [Request component options](waf-rule-statement-fields-list.md)
  + [HTTP method](waf-rule-statement-fields-list.md#waf-rule-statement-request-component-http-method)
  + [Single header](waf-rule-statement-fields-list.md#waf-rule-statement-request-component-single-header)
  + [All headers](waf-rule-statement-fields-list.md#waf-rule-statement-request-component-headers)
  + [Cookies](waf-rule-statement-fields-list.md#waf-rule-statement-request-component-cookies)
  + [URI path](waf-rule-statement-fields-list.md#waf-rule-statement-request-component-uri-path)
  + [Query string](waf-rule-statement-fields-list.md#waf-rule-statement-request-component-query-string)
  + [Single query parameter](waf-rule-statement-fields-list.md#waf-rule-statement-request-component-single-query-param)
  + [All query parameters](waf-rule-statement-fields-list.md#waf-rule-statement-request-component-all-query-params)
  + [Body](waf-rule-statement-fields-list.md#waf-rule-statement-request-component-body)
  + [JSON body](waf-rule-statement-fields-list.md#waf-rule-statement-request-component-json-body)
+ [How to inspect HTTP/2 pseudo headers](waf-rule-statement-request-components-for-http2-pseudo-headers.md)
+ [Text transformations](waf-rule-statement-transformation.md)