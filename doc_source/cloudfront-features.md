# How AWS WAF Works with Amazon CloudFront Features<a name="cloudfront-features"></a>

When you create a web ACL, you can specify one or more CloudFront distributions that you want AWS WAF to inspect\. AWS WAF starts to allow, block, or count web requests for those distributions based on the conditions that you identify in the web ACL\. CloudFront provides some features that enhance the AWS WAF functionality\. This chapter describes a few ways that you can configure CloudFront to make CloudFront and AWS WAF work better together\.

**Topics**
+ [Using AWS WAF with CloudFront Custom Error Pages](#cloudfront-features-custom-error-pages)
+ [Using AWS WAF with CloudFront Geo Restriction](#cloudfront-features-geo-restriction)
+ [Choosing the HTTP Methods That CloudFront Responds To](#cloudfront-features-allowed-http-methods)

## Using AWS WAF with CloudFront Custom Error Pages<a name="cloudfront-features-custom-error-pages"></a>

When AWS WAF blocks a web request based on the conditions that you specify, it returns HTTP status code 403 \(Forbidden\) to CloudFront\. Next, CloudFront returns that status code to the viewer\. The viewer then displays a brief and sparsely formatted default message similar to this:

`Forbidden: You don't have permission to access /myfilename.html on this server.`

If you'd rather display a custom error message, possibly using the same formatting as the rest of your website, you can configure CloudFront to return to the viewer an object \(for example, an HTML file\) that contains your custom error message\. 

**Note**  
CloudFront can't distinguish between an HTTP status code 403 that is returned by your origin and one that is returned by AWS WAF when a request is blocked\. This means that you can't return different custom error pages based on the different causes of an HTTP status code 403\. 

For more information about CloudFront custom error pages, see [Customizing Error Responses](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/custom-error-pages.html) in the *Amazon CloudFront Developer Guide*\.

## Using AWS WAF with CloudFront Geo Restriction<a name="cloudfront-features-geo-restriction"></a>

You can use the Amazon CloudFront *geo restriction* feature, also known as *geoblocking*, to prevent users in specific geographic locations from accessing content that you distribute through a CloudFront web distribution\. If you want to block web requests from specific countries and also block requests based on other conditions, you can use CloudFront geo restriction in conjunction with AWS WAF\. CloudFront returns the same HTTP status code to viewers—HTTP 403 \(Forbidden\)—whether they try to access your content from a country on a CloudFront geo restriction blacklist or whether the request is blocked by AWS WAF\. 

**Note**  
You can see the two\-letter country code of the country that requests originate from in the sample of web requests for a web ACL\. For more information, see [Viewing a Sample of the Web Requests That API Gateway CloudFront or an Application Load Balancer Has Forwarded to AWS WAF](web-acl-testing.md#web-acl-testing-view-sample)\.

For more information about CloudFront geo restriction, see [Restricting the Geographic Distribution of Your Content](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/georestrictions.html) in the *Amazon CloudFront Developer Guide*\.

## Choosing the HTTP Methods That CloudFront Responds To<a name="cloudfront-features-allowed-http-methods"></a>

When you create an Amazon CloudFront web distribution, you choose the HTTP methods that you want CloudFront to process and forward to your origin\. You can choose from the following options:
+ **GET, HEAD** – You can use CloudFront only to get objects from your origin or to get object headers\.
+ **GET, HEAD, OPTIONS** – You can use CloudFront only to get objects from your origin, get object headers, or retrieve a list of the options that your origin server supports\.
+ **GET, HEAD, OPTIONS, PUT, POST, PATCH, DELETE** – You can use CloudFront to get, add, update, and delete objects, and to get object headers\. In addition, you can perform other POST operations such as submitting data from a web form\. 

You also can use AWS WAF string match conditions to allow or block requests based on the HTTP method, as described in [Working with String Match Conditions](web-acl-string-conditions.md)\. If you want to use a combination of methods that CloudFront supports, such as `GET` and `HEAD`, then you don't need to configure AWS WAF to block requests that use the other methods\. If you want to allow a combination of methods that CloudFront doesn't support, such as `GET`, `HEAD`, and `POST`, you can configure CloudFront to respond to all methods, and then use AWS WAF to block requests that use other methods\.

For more information about choosing the methods that CloudFront responds to, see [Allowed HTTP Methods](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-values-specify.html#DownloadDistValuesAllowedHTTPMethods) in the topic [Values that You Specify When You Create or Update a Web Distribution](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-values-specify.html) in the *Amazon CloudFront Developer Guide*\.