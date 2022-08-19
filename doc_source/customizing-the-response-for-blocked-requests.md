# Custom responses for block actions<a name="customizing-the-response-for-blocked-requests"></a>

You can instruct AWS WAF to send a custom HTTP response back to the client for rule actions or web ACL default actions that are set to `Block`\. For more information about rule actions, see [AWS WAF rule action](waf-rule-action.md)\. For more information about default web ACL actions, see [Deciding on the default action for a web ACL](web-acl-default-action.md)\.

When you define custom response handling for a block action, you define the status code, headers, and response body\. For a list of status codes that you can use with AWS WAF, see the section that follows, [Supported status codes for custom response](customizing-the-response-status-codes.md)\. 

**Use cases**  
The use cases for custom responses include the following: 
+ Sending a non\-default status code back to the client\.
+ Sending a static error page back to the client\.
+ Redirecting the client to a different URL\. To do this, you specify one of the `3xx` redirection status codes, like `301 (Moved Permanently)` or `302 (Found)`, and then specify a new header named `Location` with the new URL\. 

**Interaction with responses that you define in your protected resource**  
Custom responses that you specify for the AWS WAF block action take precedence over any response specifications that you define in your protected resource\. 

The host service for the AWS resource that you protect with AWS WAF might allow custom response handling for web requests\. Examples include the following: 
+ Amazon CloudFront allows you to customize the error page based on status code\. For information, see [Generating custom error responses](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/GeneratingCustomErrorResponses.html) in the *Amazon CloudFront Developer Guide*\. 
+ Amazon API Gateway allows you to define the response and status code for your gateway\. For information, see [Gateway responses in API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-gatewayResponse-definition.html) in the *Amazon API Gateway Developer Guide*\. 

You can't combine AWS WAF custom response settings with custom response settings in the protected AWS resource\. The response specification for any individual web request comes either completely from AWS WAF or completely from the protected resource\. 

For web requests that AWS WAF blocks, the following shows the order of precedence\.

1. **AWS WAF custom response** – If the AWS WAF block action has a custom response enabled, the protected resource sends the configured custom response back to the client\. This applies whether the custom response that's define in AWS WAF specifies just the HTTP code, just a custom page, or both\. Any response settings that you might have defined in the protected resource itself have no effect\. 

1. **Custom response defined in the protected resource** – Otherwise, if the protected resource has custom response settings specified, the protected resource uses those settings to respond to the client\. 

1. **AWS WAF default block response** – Otherwise, the protected resource responds to the client with the AWS WAF default block response `403 (Forbidden)`\. 

For web requests that AWS WAF allows, your configuration of the protected resource determines the response that it sends back to the client\. You can't configure response settings in AWS WAF for allowed requests\. The only customization that you can configure in AWS WAF for allowed requests is the insertion of custom headers into the original request, before forwarding the request to the protected resource\. This option is described in the preceding section, [Custom request header insertions for allow, count, and CAPTCHA actions](customizing-the-incoming-request.md)\. 

**Custom response bodies**  
You define the body of a custom response within the context of the web ACL or rule group where you want to use it\. After you've defined a custom response body, you can use it by reference anywhere else in the web ACL or rule group where you created it\. In the individual block action settings, you reference the custom body that you want to use and you define the status code and header of the custom response\. 

When you create a custom response in the console, you can choose from response bodies that you've already defined or you can create a new body\. Outside of the console, you define your custom response bodies at the web ACL or rule group level, and then reference them from the action settings within the web ACL or rule group\. This is shown in the example JSON in the following section\. 

**Custom response example**  
The following example lists the JSON for a rule group with custom response settings\. The custom response body is defined for the entire rule group, then referenced by key in the rule action\.

```
{
 "ARN": "test_rulegroup_arn",
 "Capacity": 1,
 
 "CustomResponseBodies": {
  "CustomResponseBodyKey1": {
   "Content": "This is a plain text response body.",
   "ContentType": "TEXT_PLAIN"
  }
 },
 
 "Description": "This is a test rule group.",
 "Id": "test_rulegroup_id",
 "Name": "TestRuleGroup",
 
 "Rules": [
  {
   "Action": {
    "Block": {
     "CustomResponse": {
      "CustomResponseBodyKey": "CustomResponseBodyKey1",
      "ResponseCode": 404,
      "ResponseHeaders": [
       {
        "Name": "BlockActionHeader1Name",
        "Value": "BlockActionHeader1Value"
       }
      ]
     }
    }
   },
   "Name": "GeoMatchRule",
   "Priority": 1,
   "Statement": {
    "GeoMatchStatement": {
     "CountryCodes": [
      "US"
     ]
    }
   },
   "VisibilityConfig": {
    "CloudWatchMetricsEnabled": true,
    "MetricName": "TestRuleGroupReferenceMetric",
    "SampledRequestsEnabled": true
   }
  }
 ],
 "VisibilityConfig": {
  "CloudWatchMetricsEnabled": true,
  "MetricName": "TestRuleGroupMetric",
  "SampledRequestsEnabled": true
 }
}
```