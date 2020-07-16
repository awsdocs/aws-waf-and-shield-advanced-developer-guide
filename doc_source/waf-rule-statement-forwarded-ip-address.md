# Forwarded IP address<a name="waf-rule-statement-forwarded-ip-address"></a>

This section applies to rule statements that use the IP address of a web request\. By default, AWS WAF uses the IP address from the web request origin\. However, if a web request goes through one or more proxies or load balancers, the web request origin will contain the address of the last proxy, and not the originating address of the client\. In this case, the originating client address is usually forwarded in another HTTP header\. This header is typically `X-Forwarded-For` \(XFF\), but it can be a different one\. 

The rule statements that use IP addresses are the following:
+ [IP set match](waf-rule-statement-type-ipset-match.md) \- Inspects the IP address for a match with the addresses that are defined in an IP set\.
+ [Geographic match](waf-rule-statement-type-geo-match.md) \- Uses the IP address to determine country of origin and matches that against a list of countries\.
+ [Rate\-based](waf-rule-statement-type-rate-based.md) \- Aggregates requests by their IP addresses to ensure that no individual IP address sends requests at too high a rate\.

You can instruct AWS WAF to use a forwarded IP address for any of these rule statements, either from the `X-Forwarded-For` header or from another HTTP header, instead of using the web request's origin\. For details on how to provide the specifications, see the guidance for the individual rule statement types\.

**General considerations for using forwarded IP addresses**  
 Before you use a forwarded IP address, note the following general caveats: 
+ A header can be modified by proxies along the way, and the proxies might handle the header in different ways\. 
+ Attackers might alter the contents of the header in an attempt to bypass AWS WAF inspections\. 
+ The IP address inside the header can be malformed or invalid\.
+ The header that you specify might not be present at all in a request\.

**Considerations for using forwarded IP addresses with AWS WAF**  
The following list describes requirements and caveats for using forwarded IP addresses in AWS WAF:
+ For any single rule, you can specify one header for the forwarded IP address\. The header specification is case insensitive\.
+ For rate\-based rule statements, any nested scoping statements do not inherit the forwarded IP configuration\. Specify the configuration for each statement that uses a forwarded IP address\. 
+ For geo match and rate\-based rules, AWS WAF uses the first address in the header\. For example, if a header contains “10\.1\.1\.1, 127\.0\.0\.0, 10\.10\.10\.10”, AWS WAF uses “10\.1\.1\.1”\.
+ For IP set match, you indicate whether to match against the first, last, or any address in the header\. If you specify any, AWS WAF inspects all addresses in the header for a match, up to 10 addresses\. If the header contains more than 10 addresses, AWS WAF inspects the last 10\. 
+ Headers that contain multiple addresses must use a comma separator between the addresses\. If a request uses a separator other than a comma, AWS WAF considers the IP addresses in the header malformed\.
+ If the IP addresses inside the header are malformed or invalid, AWS WAF designates the web request as matching the rule or not matching, according to the fallback behavior that you specify in the forwarded IP configuration\. 
+ If the header that you specify isn’t present in a request, AWS WAF doesn’t apply the rule to the request at all\.
+ A rule statement that uses a forwarded IP header for the IP address won’t use the IP address that’s reported by the web request origin\.

**Best practices for using forwarded IP addresses with AWS WAF**  
When you use forwarded IP addresses, use the following best practices: 
+ Carefully consider all possible states of your request headers before enabling forwarded IP configuration\. You might need to use more than one rule to get the behavior you want\.
+ To inspect multiple forwarded IP headers or to inspect the web request origin and a forwarded IP header, use one rule for each IP address source\. 
+ To block web requests that have an invalid header, set the rule action to block and set the fallback behavior for the forwarded IP configuration to match\. 

**Example JSON for forwarded IP addresses**  
 The following geo match statement matches only if the `X-Forwarded-For` header contains an IP whose country of origin is `US`: 

```
{
  "Name": "XFFTestGeo",
  "Priority": 0,
  "Action": {
    "Block": {}
  },
  "VisibilityConfig": {
    "SampledRequestsEnabled": true,
    "CloudWatchMetricsEnabled": true,
    "MetricName": "XFFTestGeo"
  },
  "Statement": {
    "GeoMatchStatement": {
      "CountryCodes": [
        "US"
      ],
      "ForwardedIPConfig": {
        "HeaderName": "x-forwarded-for",
        "FallbackBehavior": "MATCH"
      }
    }
  }
}
```

The following rate\-based rule aggregates requests based on the first IP in the `X-Forwarded-For` header\. The rule counts only requests the match the nested geo match statement\. The nested geo match statement also uses the `X-Forwarded-For` header to determine whether the IP address indicates a country of origin of `US`\. If it does, or if the header is present but malformed, the geo match statement returns a match\. 

```
{
  "Name": "XFFTestRateGeo",
  "Priority": 0,
  "Action": {
    "Block": {}
  },
  "VisibilityConfig": {
    "SampledRequestsEnabled": true,
    "CloudWatchMetricsEnabled": true,
    "MetricName": "XFFTestRateGeo"
  },
  "Statement": {
    "RateBasedStatement": {
      "Limit": "100",
      "AggregateKeyType": "FORWARDED_IP",
      "ScopeDownStatement": {
        "GeoMatchStatement": {
          "CountryCodes": [
            "US"
          ],
          "ForwardedIPConfig": {
            "HeaderName": "x-forwarded-for",
            "FallbackBehavior": "MATCH"
          }
        }
      },
      "ForwardedIPConfig": {
        "HeaderName": "x-forwarded-for",
        "FallbackBehavior": "MATCH"
      }
    }
  }
}
```