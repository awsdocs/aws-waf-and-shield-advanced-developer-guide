# How AWS WAF Classic works with Amazon CloudFront features<a name="classic-cloudfront-features"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

When you create a web ACL, you can specify one or more CloudFront distributions that you want AWS WAF Classic to inspect\. AWS WAF Classic starts to allow, block, or count web requests for those distributions based on the conditions that you identify in the web ACL\. CloudFront provides some features that enhance the AWS WAF Classic functionality\. This chapter describes a few ways that you can configure CloudFront to make CloudFront and AWS WAF Classic work better together\.

**Topics**
+ [Using AWS WAF Classic with CloudFront custom error pages](#classic-cloudfront-features-custom-error-pages)
+ [Using AWS WAF Classic with CloudFront geo restriction](#classic-cloudfront-features-geo-restriction)
+ [Using AWS WAF Classic with CloudFront for applications running on your own HTTP server](#classic-cloudfront-features-your-own-http-server)
+ [Choosing the HTTP methods that CloudFront responds to](#classic-cloudfront-features-allowed-http-methods)

## Using AWS WAF Classic with CloudFront custom error pages<a name="classic-cloudfront-features-custom-error-pages"></a>

When AWS WAF Classic blocks a web request based on the conditions that you specify, it returns HTTP status code 403 \(Forbidden\) to CloudFront\. Next, CloudFront returns that status code to the viewer\. The viewer then displays a brief and sparsely formatted default message similar to this:

`Forbidden: You don't have permission to access /myfilename.html on this server.`

If you'd rather display a custom error message, possibly using the same formatting as the rest of your website, you can configure CloudFront to return to the viewer an object \(for example, an HTML file\) that contains your custom error message\. 

**Note**  
CloudFront can't distinguish between an HTTP status code 403 that is returned by your origin and one that is returned by AWS WAF Classic when a request is blocked\. This means that you can't return different custom error pages based on the different causes of an HTTP status code 403\. 

For more information about CloudFront custom error pages, see [Customizing Error Responses](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/custom-error-pages.html) in the *Amazon CloudFront Developer Guide*\.

## Using AWS WAF Classic with CloudFront geo restriction<a name="classic-cloudfront-features-geo-restriction"></a>

You can use the Amazon CloudFront *geo restriction* feature, also known as *geoblocking*, to prevent users in specific geographic locations from accessing content that you distribute through a CloudFront web distribution\. If you want to block web requests from specific countries and also block requests based on other conditions, you can use CloudFront geo restriction in conjunction with AWS WAF Classic\. CloudFront returns the same HTTP status code to viewers—HTTP 403 \(Forbidden\)—whether they try to access your content from a country on a CloudFront geo restriction blacklist or whether the request is blocked by AWS WAF Classic\. 

**Note**  
You can see the two\-letter country code of the country that requests originate from in the sample of web requests for a web ACL\. For more information, see [Viewing a sample of the web requests that API Gateway CloudFront or an Application Load Balancer has forwarded to AWS WAF Classic](classic-web-acl-testing.md#classic-web-acl-testing-view-sample)\.

For more information about CloudFront geo restriction, see [Restricting the Geographic Distribution of Your Content](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/georestrictions.html) in the *Amazon CloudFront Developer Guide*\.

## Using AWS WAF Classic with CloudFront for applications running on your own HTTP server<a name="classic-cloudfront-features-your-own-http-server"></a>

When you use AWS WAF Classic with CloudFront, you can protect your applications running on any HTTP webserver, whether it's a webserver that's running in Amazon Elastic Compute Cloud \(Amazon EC2\) or a webserver that you manage privately\. You can also configure CloudFront to require HTTPS between CloudFront and your own webserver, as well as between viewers and CloudFront\.

**Requiring HTTPS Between CloudFront and Your Own Webserver**  
To require HTTPS between CloudFront and your own webserver, you can use the CloudFront custom origin feature and configure the **Origin Protocol Policy** and the **Origin Domain Name **settings for specific origins\. In your CloudFront configuration, you can specify the DNS name of the server along with the port and the protocol that you want CloudFront to use when fetching objects from your origin\. You should also ensure that the SSL/TLS certificate on your custom origin server matches the origin domain name you’ve configured\. When you use your own HTTP webserver outside of AWS, you must use a certificate that is signed by a trusted third\-party certificate authority \(CA\), for example, Comodo, DigiCert, or Symantec\. For more information about requiring HTTPS for communication between CloudFront and your own webserver, see the topic [Requiring HTTPS for Communication Between CloudFront and Your Custom Origin](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/using-https-cloudfront-to-custom-origin.html) in the *Amazon CloudFront Developer Guide*\.

**Requiring HTTPS Between a Viewer and CloudFront**  
To require HTTPS between viewers and CloudFront, you can change the **Viewer Protocol Policy** for one or more cache behaviors in your CloudFront distribution\. For more information about using HTTPS between viewers and CloudFront, see the topic [Requiring HTTPS for Communication Between Viewers and CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/using-https-viewers-to-cloudfront.html) in the *Amazon CloudFront Developer Guide*\. You can also bring your own SSL certificate so viewers can connect to your CloudFront distribution over HTTPS using your own domain name, for example *https://www\.mysite\.com*\. For more information, see the topic [Configuring Alternate Domain Names and HTTPS](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/cnames-and-https-procedures.html) in the *Amazon CloudFront Developer Guide*\.

## Choosing the HTTP methods that CloudFront responds to<a name="classic-cloudfront-features-allowed-http-methods"></a>

When you create an Amazon CloudFront web distribution, you choose the HTTP methods that you want CloudFront to process and forward to your origin\. You can choose from the following options:
+ **GET, HEAD** – You can use CloudFront only to get objects from your origin or to get object headers\.
+ **GET, HEAD, OPTIONS** – You can use CloudFront only to get objects from your origin, get object headers, or retrieve a list of the options that your origin server supports\.
+ **GET, HEAD, OPTIONS, PUT, POST, PATCH, DELETE** – You can use CloudFront to get, add, update, and delete objects, and to get object headers\. In addition, you can perform other POST operations such as submitting data from a web form\. 

You also can use AWS WAF Classic string match conditions to allow or block requests based on the HTTP method, as described in [Working with string match conditions](classic-web-acl-string-conditions.md)\. If you want to use a combination of methods that CloudFront supports, such as `GET` and `HEAD`, then you don't need to configure AWS WAF Classic to block requests that use the other methods\. If you want to allow a combination of methods that CloudFront doesn't support, such as `GET`, `HEAD`, and `POST`, you can configure CloudFront to respond to all methods, and then use AWS WAF Classic to block requests that use other methods\.

For more information about choosing the methods that CloudFront responds to, see [Allowed HTTP Methods](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-values-specify.html#DownloadDistValuesAllowedHTTPMethods) in the topic [Values that You Specify When You Create or Update a Web Distribution](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-values-specify.html) in the *Amazon CloudFront Developer Guide*\.