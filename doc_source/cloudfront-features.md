# How AWS WAF works with Amazon CloudFront features<a name="cloudfront-features"></a>

When you create a web ACL, you can specify one or more CloudFront distributions that you want AWS WAF to inspect\. AWS WAF starts to inspect and manage web requests for those distributions based on the criteria that you identify in the web ACL\. CloudFront provides some features that enhance the AWS WAF functionality\. This chapter describes a few ways that you can configure CloudFront to make CloudFront and AWS WAF work better together\.

**Topics**
+ [Using AWS WAF with CloudFront custom error pages](#cloudfront-features-custom-error-pages)
+ [Using AWS WAF with CloudFront for applications running on your own HTTP server](#cloudfront-features-your-own-http-server)
+ [Choosing the HTTP methods that CloudFront responds to](#cloudfront-features-allowed-http-methods)

## Using AWS WAF with CloudFront custom error pages<a name="cloudfront-features-custom-error-pages"></a>

By default, when AWS WAF blocks a web request based on the criteria that you specify, it returns HTTP status code `403 (Forbidden)` to CloudFront, and CloudFront returns that status code to the viewer\. The viewer then displays a brief and sparsely formatted default message similar to the following:

```
Forbidden: You don't have permission to access /myfilename.html on this server.
```

You can override this behavior in your AWS WAF web ACL rules by defining custom responses\. For more information about customizing response behavior using AWS WAF rules, see [Custom responses for block actions](customizing-the-response-for-blocked-requests.md)\.

**Note**  
Responses that you customize using AWS WAF rules take precedence over any response specifications that you define in CloudFront custom error pages\. 

If you'd rather display a custom error message through CloudFront, possibly using the same formatting as the rest of your website, you can configure CloudFront to return to the viewer an object \(for example, an HTML file\) that contains your custom error message\. 

**Note**  
CloudFront can't distinguish between an HTTP status code 403 that is returned by your origin and one that is returned by AWS WAF when a request is blocked\. This means that you can't return different custom error pages based on the different causes of an HTTP status code 403\. 

For more information about CloudFront custom error pages, see [Generating custom error responses](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/GeneratingCustomErrorResponses.html) in the *Amazon CloudFront Developer Guide*\.

## Using AWS WAF with CloudFront for applications running on your own HTTP server<a name="cloudfront-features-your-own-http-server"></a>

When you use AWS WAF with CloudFront, you can protect your applications running on any HTTP webserver, whether it's a webserver that's running in Amazon Elastic Compute Cloud \(Amazon EC2\) or a webserver that you manage privately\. You can also configure CloudFront to require HTTPS between CloudFront and your own webserver, as well as between viewers and CloudFront\.

**Requiring HTTPS between CloudFront and your own webserver**  
To require HTTPS between CloudFront and your own webserver, you can use the CloudFront custom origin feature and configure the **Origin Protocol Policy** and the **Origin Domain Name **settings for specific origins\. In your CloudFront configuration, you can specify the DNS name of the server along with the port and the protocol that you want CloudFront to use when fetching objects from your origin\. You should also ensure that the SSL/TLS certificate on your custom origin server matches the origin domain name you’ve configured\. When you use your own HTTP webserver outside of AWS, you must use a certificate that is signed by a trusted third\-party certificate authority \(CA\), for example, Comodo, DigiCert, or Symantec\. For more information about requiring HTTPS for communication between CloudFront and your own webserver, see the topic [Requiring HTTPS for Communication Between CloudFront and Your Custom Origin](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/using-https-cloudfront-to-custom-origin.html) in the *Amazon CloudFront Developer Guide*\.

**Requiring HTTPS between a viewer and CloudFront**  
To require HTTPS between viewers and CloudFront, you can change the **Viewer Protocol Policy** for one or more cache behaviors in your CloudFront distribution\. For more information about using HTTPS between viewers and CloudFront, see the topic [Requiring HTTPS for Communication Between Viewers and CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/using-https-viewers-to-cloudfront.html) in the *Amazon CloudFront Developer Guide*\. You can also bring your own SSL certificate so viewers can connect to your CloudFront distribution over HTTPS using your own domain name, for example *https://www\.mysite\.com*\. For more information, see the topic [Configuring Alternate Domain Names and HTTPS](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/cnames-and-https-procedures.html) in the *Amazon CloudFront Developer Guide*\.

## Choosing the HTTP methods that CloudFront responds to<a name="cloudfront-features-allowed-http-methods"></a>

When you create an Amazon CloudFront web distribution, you choose the HTTP methods that you want CloudFront to process and forward to your origin\. You can choose from the following options:
+ **`GET`, `HEAD`** – You can use CloudFront only to get objects from your origin or to get object headers\.
+ **`GET`, `HEAD`, `OPTIONS`** – You can use CloudFront only to get objects from your origin, get object headers, or retrieve a list of the options that your origin server supports\.
+ **`GET`, `HEAD`, `OPTIONS`, `PUT`, `POST`, `PATCH`, `DELETE`** – You can use CloudFront to get, add, update, and delete objects, and to get object headers\. In addition, you can perform other `POST` operations such as submitting data from a web form\. 

You also can use AWS WAF byte match rule statements to allow or block requests based on the HTTP method, as described in [String match rule statement](waf-rule-statement-type-string-match.md)\. If you want to use a combination of methods that CloudFront supports, such as `GET` and `HEAD`, then you don't need to configure AWS WAF to block requests that use the other methods\. If you want to allow a combination of methods that CloudFront doesn't support, such as `GET`, `HEAD`, and `POST`, you can configure CloudFront to respond to all methods, and then use AWS WAF to block requests that use other methods\.

For more information about choosing the methods that CloudFront responds to, see [Allowed HTTP Methods](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-values-specify.html#DownloadDistValuesAllowedHTTPMethods) in the topic [Values that You Specify When You Create or Update a Web Distribution](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-values-specify.html) in the *Amazon CloudFront Developer Guide*\.