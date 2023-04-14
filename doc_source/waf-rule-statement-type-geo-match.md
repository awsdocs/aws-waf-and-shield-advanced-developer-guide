# Geographic match rule statement<a name="waf-rule-statement-type-geo-match"></a>

Use geographical or geo match statements to manage web requests based on country and region of origin\. 

**Note**  
For CloudFront distributions, if you use the CloudFront geo restriction feature, the feature doesn't forward blocked requests to AWS WAF\. The feature does forward allowed requests to AWS WAF\. If you want to block requests based on geography and other AWS WAF criteria, use the AWS WAF geo match statement and do not use the CloudFront geo restriction feature\. 

You can use the geo match statement for country and region matching, as follows: 
+ **Country** — Use a geo match rule by itself to manage requests based on their country of origin\. 
+ **Region** — Use a geo match rule followed by a label match rule to manage requests based on their country and region of origin\. For information about using label match rules, see [Label match rule statement](waf-rule-statement-type-label-match.md) and [Labels on web requests](waf-labels.md)\.

With the geo match statement, AWS WAF manages each web request as follows: 

1. **Determines the request's country and region codes** — AWS WAF determines the country and region of a request based on its IP address\. By default, AWS WAF uses the IP address of the web request's origin\. You can instruct AWS WAF to use an IP address from an alternate request header, like `X-Forwarded-For`, by enabling forwarded IP configuration in the rule statement settings\. 

   AWS WAF uses the alpha\-2 country and region codes from the International Organization for Standardization \(ISO\) 3166 standard\. You can find the codes at the following locations:
   + At the ISO website, you can search the country codes at [ISO Online Browsing Platform \(OBP\)](https://www.iso.org/obp/ui#home)\. 
   + On Wikipedia, the country codes are listed at [ISO 3166\-2](https://en.wikipedia.org/wiki/ISO_3166-2)\.

     The region codes for a country are listed at the URL `https://en.wikipedia.org/wiki/ISO_3166-2:<ISO country code>`\. For example, the regions for the United States are at [ISO 3166\-2:US](https://en.wikipedia.org/wiki/ISO_3166-2:US) and for Ukraine they're at [ISO 3166\-2:UA](https://en.wikipedia.org/wiki/ISO_3166-2:UA)\.

1. **Determines the country label and region label to add to the request** — The labels indicate whether the geo match statement uses the origin IP or a forwarded IP configuration\.
   + **Origin IP** 

     The country label is `awswaf:clientip:geo:country:<ISO country code>`\. Example for the United States: `awswaf:clientip:geo:country:US`\.

     The region label is `awswaf:clientip:geo:region:<ISO country code>-<ISO region code>`\. Example for Oregon in the United States: `awswaf:clientip:geo:region:US-OR`\.
   + **Forwarded IP** 

     The country label is `awswaf:forwardedip:geo:country:<ISO country code>`\. Example for the United States: `awswaf:forwardedip:geo:country:US`\.

     The region label is `awswaf:forwardedip:geo:region:<ISO country code>-<ISO region code>`\. Example for Oregon in the United States: `awswaf:forwardedip:geo:region:US-OR`\.

   If the country or region code isn't available for a request's specified IP address, AWS WAF uses `XX` in the labels, in the place of the value\. For example, the following label is for a client IP whose country code isn't available: `awswaf:clientip:geo:country:XX` and the following is for a forwarded IP whose country is the United States, but whose region code isn't available: `awswaf:forwardedip:geo:region:US-XX`\. 

1. **Evaluates the request's country code against the rule criteria** 

The geo match statement adds country and region labels to all requests that it inspects, regardless of whether it finds a match\. 

**Note**  
AWS WAF adds any labels at the end of a rule's web request evaluation\. Because of this, any label matching that you use against the labels from a geo match statement must be defined in a separate rule from the geo match statement rule\. 

If you want to inspect only region values, you can write a geo match rule with Count action and with a single country code match, followed by a label match rule for the region labels\. You are required to supply a country code for the geo match rule to evaluate, even for this approach\. You can reduce logging and count metrics by specifying a country that's very unlikely to be a source of traffic to your site\. 

**Nestable** – You can nest this statement type\. 

**WCUs ** – 1 WCU\.

**Settings** – This statement uses the following settings: 
+ **Country codes** – An array of country codes to compare for a geo match\. These must be two\-character country codes from the alpha\-2 country ISO codes of the ISO 3166 international standard, for example, `["US","CN"]`\. 
+ **\(Optional\) Forwarded IP configuration** – By default, AWS WAF uses the IP address in the web request origin to determine country of origin\. Alternatively, you can configure the rule to use a forwarded IP in an HTTP header like `X-Forwarded-For` instead\. AWS WAF uses the first IP address in the header\. With this configuration, you also specify a fallback behavior to apply to a web request with a malformed IP address in the specified header\. The fallback behavior sets the matching result for the request, to match or no match\. For more information, see [Forwarded IP address](waf-rule-statement-forwarded-ip-address.md)\. 

**Where to find this rule statement**
+ **Rule builder** on the console – For **Request option**, choose **Originates from a country in**\.
+ **API** – [GeoMatchStatement](https://docs.aws.amazon.com/waf/latest/APIReference/API_GeoMatchStatement.html)

**Examples**  
You can use the geo match statement to manage requests from specific countries or regions\. For example, if you want to block requests from certain countries, but still allow requests from a specific set of IP addresses in those countries, you could create a rule with the action set to Block and the following nested statements, shown in pseudocode:
+ AND statement
  + Geo match statement listing the countries that you want to block
  + NOT statement 
    + IP set statement that specifies the IP addresses that you want to allow through

Or, if you want to block some regions in certain countries, but still allow requests from other regions in those countries, you could first define a geo match rule with the action set to Count\. Then, define a label match rule that matches against the added geo match labels and handles the requests as you need\. 

The following pseudo code describes an example of this approach:

1. Geo match statement listing the countries with regions that you want to block, but with the action set to Count\. This labels every web request regardless of match status, and it also gives you count metrics for the countries of interest\. 

1. `AND` statement with Block action
   + Label match statement that specifies the labels for the countries that you want to block
   + `NOT` statement 
     + Label match statement that specifies the labels of the regions in those countries that you want to allow through

The following JSON listing shows an implementation of the two rules described in the prior pseudocode\. These rules block all traffic from the United States except for traffic from Oregon and Washington\. The geo match statement adds country and region labels to all requests that it inspects\. The label match rule runs after the geo match rule, so it can match against the country and region labels that the geo match rule has just added\. The geo match statement uses a forwarded IP address, so the label matching also specifies forwarded IP labels\. 

```
{
   "Name": "geoMatchForLabels",
   "Priority": 10,
   "Statement": {
     "GeoMatchStatement": {
       "CountryCodes": [
         "US"
       ],
       "ForwardedIPConfig": {
           "HeaderName": "X-Forwarded-For",
           "FallbackBehavior": "MATCH"
       }
     }
   },
   "Action": {
     "Count": {}
   },
   "VisibilityConfig": {
     "SampledRequestsEnabled": true,
     "CloudWatchMetricsEnabled": true,
     "MetricName": "geoMatchForLabels"
   }
},
{
   "Name": "blockUSButNotOROrWA",
   "Priority": 11,
   "Statement": {
     "AndStatement": {
       "Statements": [
         {
           "LabelMatchStatement": {
             "Scope": "LABEL",
             "Key": "awswaf:forwardedip:geo:country:US"
           }
         },
         {
           "NotStatement": {
             "Statement": {
                "OrStatement": {
                  "Statements": [
                    {
                       "LabelMatchStatement": {
                         "Scope": "LABEL",
                         "Key": "awswaf:forwardedip:geo:region:US-OR"
                       }
                    },
                    {
                       "LabelMatchStatement": {
                         "Scope": "LABEL",
                         "Key": "awswaf:forwardedip:geo:region:US-WA"
                       }
                    }
                 ]
               }
             }
           }
         }
       ]
     }
   },
   "Action": {
     "Block": {}
   },
   "VisibilityConfig": {
     "SampledRequestsEnabled": true,
     "CloudWatchMetricsEnabled": true,
     "MetricName": "blockUSButNotOROrWA"
   }
}
```

As another example, you can combine geo matching with rate\-based rules to prioritize resources for users in a particular country or region\. You create a different rate\-based statement for each geo match or label match statement that you use to differentiate your users\. Set a higher rate limit for users in the preferred country or region and set a lower rate limit for other users\. 

The following JSON listing shows a geo match rule followed by rate\-based rules that limit the rate of traffic from the United States\. The rules allow traffic from Oregon to come in at a higher rate than traffic from anywhere else in the country\. 

```
{
  "Name": "geoMatchForLabels",
  "Priority": 190,
  "Statement": {
    "GeoMatchStatement": {
      "CountryCodes": [
        "US"
      ]
    }
  },
  "Action": {
    "Count": {}
  },
  "VisibilityConfig": {
    "SampledRequestsEnabled": true,
    "CloudWatchMetricsEnabled": true,
    "MetricName": "geoMatchForLabels"
  }
},
{
  "Name": "rateLimitOregon",
  "Priority": 195,
  "Statement": {
    "RateBasedStatement": {
      "Limit": 3000,
      "AggregateKeyType": "IP",
      "ScopeDownStatement": {
        "LabelMatchStatement": {
          "Scope": "LABEL",
          "Key": "awswaf:clientip:geo:region:US-OR"
        }
      }
    }
  },
  "Action": {
    "Block": {}
  },
  "VisibilityConfig": {
    "SampledRequestsEnabled": true,
    "CloudWatchMetricsEnabled": true,
    "MetricName": "rateLimitOregon"
  }
},
{
  "Name": "rateLimitUSNotOR",
  "Priority": 200,
  "Statement": {
    "RateBasedStatement": {
      "Limit": 100,
      "AggregateKeyType": "IP",
      "ScopeDownStatement": {
        "AndStatement": {
          "Statements": [
            {
              "LabelMatchStatement": {
                "Scope": "LABEL",
                "Key": "awswaf:clientip:geo:country:US"
              }
            },
            {
              "NotStatement": {
                "Statement": {
                  "LabelMatchStatement": {
                    "Scope": "LABEL",
                    "Key": "awswaf:clientip:geo:region:US-OR"
                  }
                }
              }
            }
          ]
        }
      }
    }
  },
  "Action": {
    "Block": {}
  },
  "VisibilityConfig": {
    "SampledRequestsEnabled": true,
    "CloudWatchMetricsEnabled": true,
    "MetricName": "rateLimitUSNotOR"
  }
}
```