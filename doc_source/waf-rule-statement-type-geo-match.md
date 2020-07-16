# Geographic match rule statement<a name="waf-rule-statement-type-geo-match"></a>

To allow or block web requests based on country of origin, create one or more geographical, or geo, match statements\. 

**Note**  
If you use the CloudFront geo restriction feature to block a country from accessing your content, any request from that country is blocked and is not forwarded to AWS WAF\. So if you want to allow or block requests based on geography plus other AWS WAF criteria, you should *not* use the CloudFront geo restriction feature\. Instead, you should use an AWS WAF geo match condition\.

You can use this to block access to your site from specific countries or to only allow access from specific countries\. If you want to allow some web requests and block others based on country of origin, add a geo match statement for the countries that you want to allow and add a second one for the countries that you want to block\. 

You can use geo match statements with other AWS WAF statements to build sophisticated filtering\. For example, to block certain countries, but still allow requests from a specific set of IP addresses in that country, you could create a rule with the action set to `Block` and the following nested statements:
+ AND statement
  + Geo match statement listing the countries that you want to block
  + NOT statement 
    + IP set statement that specifies the IP addresses that you want to allow through

As another example, if you want to prioritize resources for users in a particular country, you could create a different rate\-based rules statement for each geo match condition\. Set a higher rate limit for users in the preferred country and set a lower rate limit for all other users\.

AWS WAF determines the country of origin by resolving the IP address of the web request's origin\. If you want to instead use an IP address from an alternate header, like `X-Forwarded-For`, enable forwarded IP configuration\.

**Nestable** – You can nest this statement type inside logical rule statements and rate\-based statements\. 

**WCUs ** – 1 WCU\.

This statement uses the following settings: 
+ **Geo match ** – An array of country codes to compare for a geo match\. These must be two\-character country codes, for example, `[ "US", "CN" ]`, from the alpha\-2 country ISO codes of the ISO 3166 international standard\. 

  Each code must be one or two characters long\. 
+ **\(Optional\) Forwarded IP configuration** – By default, AWS WAF uses the IP address in the web request origin to determine country of origin\. Alternatively, you can configure the rule to use a forwarded IP in an HTTP header like `X-Forwarded-For` instead\. AWS WAF uses the first IP address in the header\. With this configuration, you also specify a fallback behavior to apply to a web request with a malformed IP address in the specified header\. The fallback behavior sets the matching result for the request, to match or no match\. For more information, see [Forwarded IP address](waf-rule-statement-forwarded-ip-address.md)\. 

**Where to find this**
+ **Rule builder** on the console – For **Request option**, choose **Originates from a country in**\.
+ **API statement** – `GeoMatchStatement`