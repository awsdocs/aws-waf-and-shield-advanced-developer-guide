# Making HTTPS requests to AWS WAF or Shield Advanced<a name="waf-api-making-requests"></a>

AWS WAF and Shield Advanced requests are HTTPS requests, as defined by [RFC 2616](http://tools.ietf.org/html/rfc2616)\. Like any HTTP request, a request to AWS WAF or Shield Advanced contains a request method, a URI, request headers, and a request body\. The response contains an HTTP status code, response headers, and sometimes a response body\.

## Request URI<a name="waf-api-making-requests-uri"></a>

The request URI is always a single forward slash, `/`\.

## HTTP headers<a name="waf-api-making-requests-header"></a>

AWS WAF and Shield Advanced require the following information in the header of an HTTP request:

**Host \(Required\)**  
The endpoint that specifies where your resources are created\. For information about endpoints, see [AWS service endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html)\. For example, the value of the `Host` header for AWS WAF for a CloudFront distribution is `waf.amazonaws.com:443`\.

**x\-amz\-date or Date \(Required\)**  
The date used to create the signature that is contained in the `Authorization` header\. Specify the date in ISO 8601 standard format, in UTC time, as shown in the following example:  

```
x-amz-date: 20151007T174952Z
```
You must include either `x-amz-date` or `Date`\. \(Some HTTP client libraries don't let you set the `Date` header\)\. When an `x-amz-date` header is present, AWS WAF ignores any `Date` header when authenticating the request\.  
The time stamp must be within 15 minutes of the AWS system time when the request is received\. If it isn't, the request fails with the `RequestExpired` error code to prevent someone else from replaying your requests\.

**Authorization \(Required\)**  
The information required for request authentication\. For more information about constructing this header, see [Authenticating requests](authenticating-requests.md)\.

**X\-Amz\-Target \(Required\)**  
A concatenation of `AWSWAF_` or `AWSShield_`, the API version without punctuation, a period \(`.`\), and the name of the operation, for example:  
`AWSWAF_20150824.CreateWebACL`

**Content\-Type \(Conditional\)**  
Specifies that the content type is JSON as well as the version of JSON, as shown in the following example:  

```
Content-Type: application/x-amz-json-1.1
```
Condition: Required for POST requests\.

**Content\-Length \(Conditional\)**  
Length of the message \(without the headers\) according to RFC 2616\.  
Condition: Required if the request body itself contains information \(most toolkits add this header automatically\)\.

The following is an example header for an HTTP request to create a web ACL in AWS WAF:

```
POST / HTTP/1.1
Host: waf.amazonaws.com:443
X-Amz-Date: 20151007T174952Z
Authorization: AWS4-HMAC-SHA256 
               Credential=AccessKeyID/20151007/us-east-2/waf/aws4_request,
               SignedHeaders=host;x-amz-date;x-amz-target,
               Signature=145b1567ab3c50d929412f28f52c45dbf1e63ec5c66023d232a539a4afd11fd9
X-Amz-Target: AWSWAF_20150824.CreateWebACL
Accept: */*
Content-Type: application/x-amz-json-1.1; charset=UTF-8
Content-Length: 231
Connection: Keep-Alive
```

## HTTP request body<a name="waf-api-making-requests-body"></a>

Many AWS WAF and Shield Advanced API actions require you to include JSON\-formatted data in the body of the request\.

The following example request uses a simple JSON statement to update an `IPSet` \(known in the console as an IP match condition\) to include the IP address 192\.0\.2\.44 \(represented in CIDR notation as 192\.0\.2\.44/32\):

```
POST / HTTP/1.1
Host: waf.amazonaws.com:443
X-Amz-Date: 20151007T174952Z
Authorization: AWS4-HMAC-SHA256 
               Credential=AccessKeyID/20151007/us-east-2/waf/aws4_request,
               SignedHeaders=host;x-amz-date;x-amz-target,
               Signature=145b1567ab3c50d929412f28f52c45dbf1e63ec5c66023d232a539a4afd11fd9
X-Amz-Target: AWSWAF_20150824.UpdateIPSet
Accept: */*
Content-Type: application/x-amz-json-1.1; charset=UTF-8
Content-Length: 283
Connection: Keep-Alive

{
   "ChangeToken": "d4c4f53b-9c7e-47ce-9140-0ee5ffffffff",
   "IPSetId": "69d4d072-170c-463d-ab82-0643ffffffff",
   "Updates": [
      {
         "Action": "INSERT",
         "IPSetDescriptor": {
            "Type": "IPV4",
            "Value": "192.0.2.44/32"
         }
      }
   ]
}
```