# Logging web ACL traffic information<a name="logging"></a>

You can enable logging to get detailed information about traffic that is analyzed by your web ACL\. Information that is contained in the logs includes the time that AWS WAF received the request from your AWS resource, detailed information about the request, and the action for the rule that each request matched\. 

In the logging configuration for your web ACL, you can customize what AWS WAF sends to the logs as follows:
+ **Log filtering** – You can add filtering to specify which web requests are kept in the logs and which are dropped\. You can filter on the rule action and on the web request labels that were applied during the request evaluation\. For information about rule action settings, see [AWS WAF rule action](waf-rule-action.md)\. For information about labels, see [AWS WAF labels on web requests](waf-rule-labels.md)\.
+ **Field redaction** – You can redact some fields from the log records\. Redacted fields appear as `XXX` in the logs\. For example, if you redact the **URI** field, the **URI** field in the logs will be `XXX`\. For a list of the log fields, see [Log Fields](#logging-fields)\.

You send logs from your web ACL to an Amazon Kinesis Data Firehose with a configured storage destination\. After you enable logging, AWS WAF delivers logs to your storage destination through the HTTPS endpoint of Kinesis Data Firehose\. 

For information about how to create an Amazon Kinesis Data Firehose and review your stored logs, see [What Is Amazon Kinesis Data Firehose?](https://docs.aws.amazon.com/firehose/latest/dev/what-is-this-service.html) To understand the permissions required for your Kinesis Data Firehose configuration, see [Controlling Access with Amazon Kinesis Data Firehose](https://docs.aws.amazon.com/firehose/latest/dev/controlling-access.html)\.

You must have the following permissions to successfully enable logging:
+ `iam:CreateServiceLinkedRole`
+ `firehose:ListDeliveryStreams`
+ `wafv2:PutLoggingConfiguration`

For more information about service\-linked roles and the `iam:CreateServiceLinkedRole` permission, see [Using service\-linked roles for AWS WAF](using-service-linked-roles.md)\.

## Managing logging for a web ACL<a name="logging-management"></a>

You can enable and disable logging for a web ACL at any time\.<a name="logging-procedure"></a>

**To enable logging for a web ACL**

1. Create an Amazon Kinesis Data Firehose using a name starting with the prefix `aws-waf-logs-`\. For example, `aws-waf-logs-us-east-2-analytics`\. Create the data firehose with a `PUT` source and in the region that you are operating\. If you are capturing logs for Amazon CloudFront, create the firehose in US East \(N\. Virginia\)\. For more information, see [Creating an Amazon Kinesis Data Firehose Delivery Stream](https://docs.aws.amazon.com/firehose/latest/dev/basic-create.html)\.
**Important**  
Do not choose `Kinesis stream` as your source\.  
One AWS WAF log is equivalent to one Kinesis Data Firehose record\. If you typically receive 10,000 requests per second and you enable full logs, you should have a 10,000 records per second setting in Kinesis Data Firehose\. If you don't configure Kinesis Data Firehose correctly, AWS WAF won't record all logs\. For more information, see [Amazon Kinesis Data Firehose Quotas](https://docs.aws.amazon.com/firehose/latest/dev/limits.html)\. 

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Web ACLs**\.

1. Choose the web ACL that you want to enable logging for\.

1. On the **Logging** tab, choose **Enable logging**\.

1. Choose the Kinesis Data Firehose that you created in the first step\. You must choose a firehose that begins with `aws-waf-logs-`\.

1. \(Optional\) If you don't want certain fields and their values included in the logs, redact those fields\. Choose the field to redact, and then choose **Add**\. Repeat as necessary to redact additional fields\. The redacted fields appear as `XXX` in the logs\. For example, if you redact the **URI** field, the **URI** field in the logs will be `XXX`\. 

1. \(Optional\) If you don't want to send all requests to the logs, add your filtering criteria and behavior\. Under **Filter logs**, for each filter that you want to apply, choose **Add filter**, then choose your filtering criteria and specify whether you want to keep or drop requests that match the criteria\. When you finish adding filters, if needed, modify the **Default logging behavior**\. 

1. Choose **Enable logging**\.
**Note**  
When you successfully enable logging, AWS WAF will create a service linked role with the necessary permissions to write logs to the Amazon Kinesis Data Firehose\. For more information, see [Using service\-linked roles for AWS WAF](using-service-linked-roles.md)\.

**To disable logging for a web ACL**

1. In the navigation pane, choose **Web ACLs**\.

1. Choose the web ACL that you want to disable logging for\.

1. On the **Logging** tab, choose **Disable logging**\.

1. In the dialog box, choose **Disable logging**\.

## Log Fields<a name="logging-fields"></a>

The following list describes the possible log fields\. 

**action**  
The action\. `ALLOW` and `BLOCK` are terminating rule actions\. `COUNT` is a non\-terminating rule action\. `CAPTCHA` is non\-terminating if the request includes a valid CAPTCHA token and terminating if it doesn't\. 

**args**  
The query string\.

**captchaResponse**  
The CAPTCHA response to the request, populated when the CAPTCHA action results in the termination of web request inspection\. The CAPTCHA action terminates web request inspection when the request either doesn't include a CAPTCHA token or the token is invalid or expired\. This field includes a response code and a failure reason\. When a CAPTCHA action results in the web request being allowed, the information is captured in the field `nonTerminatingMatchingRules`\.

**clientIp**  
The IP address of the client sending the request\.

**country**  
The source country of the request\. If AWS WAF is unable to determine the country of origin, it sets this field to `-`\. 

**excludedRules**  
The list of rules in the rule group that you have excluded\. The action for these rules is set to COUNT\.    
exclusionType  
A type that indicates that the excluded rule has the action COUNT\.  
ruleId  
The ID of the rule within the rule group that is excluded\.

**formatVersion**  
The format version for the log\.

**headers**  
The list of headers\.

**httpMethod**  
The HTTP method in the request\.

**httpRequest**  
The metadata about the request\.

**httpSourceId**  
The source ID\. This field shows the ID of the associated resource\. 

**httpSourceName**  
The source of the request\. Possible values: `CF` for Amazon CloudFront, `APIGW` for Amazon API Gateway, `ALB` for Application Load Balancer, and `APPSYNC` for AWS AppSync\.

**httpVersion**  
The HTTP version\.

**labels**  
The labels on the web request\. These labels were applied by rules that were used to evaluate the request\. 

**limitKey**  
Indicates the IP address source that AWS WAF should use to aggregate requests for rate limiting by a rate\-based rule\. Possible values are `IP`, for web request origin, and `FORWARDED_IP`, for an IP forwarded in a header in the request\.

**limitValue**  
The IP address used by a rate\-based rule to aggregate requests for rate limiting\. If a request contains an IP address that isn't valid, the `limitvalue` is `INVALID`\.

**maxRateAllowed**  
The maximum number of requests, which have an identical value in the field that is specified by `limitKey`, allowed in a five\-minute period\. If the number of requests exceeds the `maxRateAllowed` and the other predicates specified in the rule are also met, AWS WAF triggers the action that is specified for this rule\.

**nonTerminatingMatchingRules**  
The list of non\-terminating rules in the rule group that match the request\.     
action  
This is either `COUNT` or `CAPTCHA`\. The CAPTCHA action is non\-terminating when the web request contains a valid CAPTCHA token\.  
ruleId  
The ID of the rule within the rule group that matches the request and was non\-terminating\.   
ruleMatchDetails  
Detailed information about the rule that matched the request\. This field is only populated for SQL injection and cross\-site scripting \(XSS\) match rule statements\. 

**rateBasedRuleId**  
The ID of the rate\-based rule that acted on the request\. If this has terminated the request, the ID for `rateBasedRuleId` is the same as the ID for `terminatingRuleId`\.

**rateBasedRuleList**  
The list of rate\-based rules that acted on the request\.

**requestHeadersInserted**  
The list of headers inserted for custom request handling\.

**requestId**  
The ID of the request, which is generated by the underlying host service\. For Application Load Balancer, this is the trace ID\. For all others, this is the request ID\. 

**responseCodeSent**  
The response code sent with a custom response\.

**ruleGroupId**  
The ID of the rule group\. If the rule blocked the request, the ID for `ruleGroupID` is the same as the ID for `terminatingRuleId`\. 

**ruleGroupList**  
The list of rule groups that acted on this request\. 

**terminatingRule**  
The rule within the rule group that terminated the request\. If this is a non\-null value, it also contains a **ruleId** and **action**\. 

**terminatingRuleId**  
The ID of the rule that terminated the request\. If nothing terminates the request, the value is `Default_Action`\.

**terminatingRuleMatchDetails**  
Detailed information about the terminating rule that matched the request\. A terminating rule has an action that ends the inspection process against a web request\. Possible actions for a terminating rule are `ALLOW`, `BLOCK`, and `CAPTCHA`\. The matching rule might have more than one inspection criteria that must be met, so the details for the terminating rule are provided as an array of match criteria\. This is only populated for SQL injection and cross\-site scripting \(XSS\) match rule statements\. As with all rule statements that inspect for more than one thing, AWS WAF applies the action on the first match and stops inspecting the web request\. A web request with a terminating action could contain other threats, in addition to the one reported in the log\.

**terminatingRuleType**  
The type of rule that terminated the request\. Possible values: RATE\_BASED, REGULAR, GROUP, and MANAGED\_RULE\_GROUP\.

**timestamp**  
The timestamp in milliseconds\.

**uri**  
The URI of the request\. The preceding code example demonstrates what the value would be if this field had been redacted\.

**webaclId**  
The GUID of the web ACL\.

## Log Examples<a name="logging-examples"></a>

**Example Log output for a rule that triggered on SQLi detection \(terminating\)**  

```
{
    "timestamp": 1576280412771,
    "formatVersion": 1,
    "webaclId": "arn:aws:wafv2:ap-southeast-2:111122223333:regional/webacl/STMTest/1EXAMPLE-2ARN-3ARN-4ARN-123456EXAMPLE",
    "terminatingRuleId": "STMTest_SQLi_XSS",
    "terminatingRuleType": "REGULAR",
    "action": "BLOCK",
    "terminatingRuleMatchDetails": [
        {
            "conditionType": "SQL_INJECTION",
            "location": "HEADER",
            "matchedData": [
                "10",
                "AND",
                "1"
            ]
        }
    ],
    "httpSourceName": "-",
    "httpSourceId": "-",
    "ruleGroupList": [],
    "rateBasedRuleList": [],
    "nonTerminatingMatchingRules": [],
    "httpRequest": {
        "clientIp": "1.1.1.1",
        "country": "AU",
        "headers": [
            {
                "name": "Host",
                "value": "localhost:1989"
            },
            {
                "name": "User-Agent",
                "value": "curl/7.61.1"
            },
            {
                "name": "Accept",
                "value": "*/*"
            },
            {
                "name": "x-stm-test",
                "value": "10 AND 1=1"
            }
        ],
        "uri": "/foo",
        "args": "",
        "httpVersion": "HTTP/1.1",
        "httpMethod": "GET",
        "requestId": "rid"
    },
    "labels": [
        {
            "name": "value"
        }
    ]
}
```

**Example Log output for a rule that triggered on SQLi detection \(non\-terminating\)**  

```
{
    "timestamp":1592357192516
    ,"formatVersion":1
    ,"webaclId":"arn:aws:wafv2:us-east-1:123456789012:global/webacl/hello-world/5933d6d9-9dde-js82-v8aw-9ck28nv9"
    ,"terminatingRuleId":"Default_Action"
    ,"terminatingRuleType":"REGULAR"
    ,"action":"ALLOW"
    ,"terminatingRuleMatchDetails":[]
    ,"httpSourceName":"-"
    ,"httpSourceId":"-"
    ,"ruleGroupList":[]
    ,"rateBasedRuleList":[]
    ,"nonTerminatingMatchingRules":
    [{
        "ruleId":"TestRule"
        ,"action":"COUNT"
        ,"ruleMatchDetails":
        [{
            "conditionType":"SQL_INJECTION"
            ,"location":"HEADER"
            ,"matchedData":[
                "10"
                ,"and"
                ,"1"]
            }]
    }]
    ,"httpRequest":{
        "clientIp":"3.3.3.3"
        ,"country":"US"
        ,"headers":[
            {"name":"Host","value":"localhost:1989"}
            ,{"name":"User-Agent","value":"curl/7.61.1"}
            ,{"name":"Accept","value":"*/*"}
            ,{"name":"foo","value":"10 AND 1=1"}
            ]
            ,"uri":"/foo","args":""
            ,"httpVersion":"HTTP/1.1"
            ,"httpMethod":"GET"
            ,"requestId":"rid"
    },
    "labels": [
        {
            "name": "value"
        }
    ]
}
```

**Example Log output for multiple rules that triggered inside a rule group \(RuleA\-XSS is terminating and Rule\-B is non\-terminating\)**  

```
{
    "timestamp":1592361810888,
    "formatVersion":1,
    "webaclId":"arn:aws:wafv2:us-east-1:123456789012:global/webacl/hello-world/5933d6d9-9dde-js82-v8aw-9ck28nv9"
    ,"terminatingRuleId":"RG-Reference"
    ,"terminatingRuleType":"GROUP"
    ,"action":"BLOCK",
    "terminatingRuleMatchDetails":
    [{
        "conditionType":"XSS"
        ,"location":"HEADER"
        ,"matchedData":["<","frameset"]
    }]
    ,"httpSourceName":"-"
    ,"httpSourceId":"-"
    ,"ruleGroupList":
    [{
        "ruleGroupId":"arn:aws:wafv2:us-east-1:123456789012:global/rulegroup/hello-world/c05lb698-1f11-4m41-aef4-99a506d53f4b"
        ,"terminatingRule":{
            "ruleId":"RuleA-XSS"
            ,"action":"BLOCK"
            ,"ruleMatchDetails":null
            }
        ,"nonTerminatingMatchingRules":
        [{
            "ruleId":"RuleB-SQLi"
            ,"action":"COUNT"
            ,"ruleMatchDetails":
            [{
                "conditionType":"SQL_INJECTION"
                ,"location":"HEADER"
                ,"matchedData":[
                    "10"
                    ,"and"
                    ,"1"]
            }]
        }]
        ,"excludedRules":null
    }]
    ,"rateBasedRuleList":[]
    ,"nonTerminatingMatchingRules":[]
    ,"httpRequest":{
        "clientIp":"3.3.3.3"
        ,"country":"US"
        ,"headers":
        [
            {"name":"Host","value":"localhost:1989"}
            ,{"name":"User-Agent","value":"curl/7.61.1"}
            ,{"name":"Accept","value":"*/*"}
            ,{"name":"xssfoo","value":"<frameset onload=alert(1)>"}
            ,{"name":"bar","value":"10 AND 1=1"}
            ]
        ,"uri":"/foo"
        ,"args":""
        ,"httpVersion":"HTTP/1.1"
        ,"httpMethod":"GET"
        ,"requestId":"rid"
    },
    "labels": [
        {
            "name": "value"
        }
    ]
}
```

**Example Log output for a rule that triggered for the inspection of the request body with content type JSON**  
AWS WAF currently reports the location for JSON body inspection as `UNKNOWN`\.  

```
{
    "timestamp": 1576280412771,
    "formatVersion": 1,
    "webaclId": "arn:aws:wafv2:ap-southeast-2:123456789012:regional/webacl/test/111",
    "terminatingRuleId": "STMTest_SQLi_XSS",
    "terminatingRuleType": "REGULAR",
    "action": "BLOCK",
    "terminatingRuleMatchDetails": [
        {
            "conditionType": "SQL_INJECTION",
            "location": "UNKNOWN",
            "matchedData": [
                "10",
                "AND",
                "1"
            ]
        }
    ],
    "httpSourceName": "ALB",
    "httpSourceId": "alb",
    "ruleGroupList": [],
    "rateBasedRuleList": [],
    "nonTerminatingMatchingRules": [],
    "requestHeadersInserted":null,
    "responseCodeSent":null,
    "httpRequest": {
        "clientIp": "1.1.1.1",
        "country": "AU",
        "headers": [],
        "uri": "",
        "args": "",
        "httpVersion": "HTTP/1.1",
        "httpMethod": "POST",
        "requestId": "null"
    },
    "labels": [
        {
            "name": "value"
        }
    ]
}
```

**Example Log output for a CAPTCHA rule against a web request with a valid, unexpired CAPTCHA token**  
The following log listing is for a web request that matched a rule with CAPTCHA action\. The web request has a valid and unexpired CAPTCHA token, and is only noted as a CAPTCHA match by AWS WAF, similar to a Count action\. This CAPTCHA match is noted under `nonTerminatingMatchingRules`\.  

```
{
  "timestamp": 1632420429309,
  "formatVersion": 1,
  "webaclId": "arn:aws:wafv2:us-east-1:123456789012:regional/webacl/captcha-web-acl/585e38b5-afce-4d2a-b417-14fb08b66c67",
  "terminatingRuleId": "Default_Action",
  "terminatingRuleType": "REGULAR",
  "action": "ALLOW",
  "terminatingRuleMatchDetails": [],
  "httpSourceName": "APIGW",
  "httpSourceId": "123456789012:b34myvfw0b:pen-test",
  "ruleGroupList": [],
  "rateBasedRuleList": [],
  "nonTerminatingMatchingRules": [
    {
      "ruleId": "captcha-rule",
      "action": "CAPTCHA",
      "ruleMatchDetails": [],
      "captchaResponse": {
        "responseCode": 0,
        "solveTimestamp": 1632420429
      }
    }
  ],
  "requestHeadersInserted": [
    {
      "name": "x-amzn-waf-test-header-name",
      "value": "test-header-value"
    }
  ],
  "responseCodeSent": null,
  "httpRequest": {
    "clientIp": "72.21.198.65",
    "country": "US",
    "headers": [
      {
        "name": "X-Forwarded-For",
        "value": "72.21.198.65"
      },
      {
        "name": "X-Forwarded-Proto",
        "value": "https"
      },
      {
        "name": "X-Forwarded-Port",
        "value": "443"
      },
      {
        "name": "Host",
        "value": "b34myvfw0b.gamma.execute-api.us-east-1.amazonaws.com"
      },
      {
        "name": "X-Amzn-Trace-Id",
        "value": "Root=1-614cc24d-5ad89a09181910c43917a888"
      },
      {
        "name": "cache-control",
        "value": "max-age=0"
      },
      {
        "name": "sec-ch-ua",
        "value": "\"Chromium\";v=\"94\", \"Google Chrome\";v=\"94\", \";Not A Brand\";v=\"99\""
      },
      {
        "name": "sec-ch-ua-mobile",
        "value": "?0"
      },
      {
        "name": "sec-ch-ua-platform",
        "value": "\"Windows\""
      },
      {
        "name": "upgrade-insecure-requests",
        "value": "1"
      },
      {
        "name": "user-agent",
        "value": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.54 Safari/537.36"
      },
      {
        "name": "accept",
        "value": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9"
      },
      {
        "name": "sec-fetch-site",
        "value": "same-origin"
      },
      {
        "name": "sec-fetch-mode",
        "value": "navigate"
      },
      {
        "name": "sec-fetch-user",
        "value": "?1"
      },
      {
        "name": "sec-fetch-dest",
        "value": "document"
      },
      {
        "name": "referer",
        "value": "https://b34myvfw0b.gamma.execute-api.us-east-1.amazonaws.com/pen-test/pets"
      },
      {
        "name": "accept-encoding",
        "value": "gzip, deflate, br"
      },
      {
        "name": "accept-language",
        "value": "en-US,en;q=0.9"
      },
      {
        "name": "cookie",
        "value": "aws-waf-token=51c71352-41f5-4f6d-b676-c24907bdf819:EQoAZ/J+AAQAAAAA:t9wvxbw042wva7E2Y6lgud/bS6YG0CJKVAJqaRqDZ140ythKW0Zj9wKB2O8lSkYDRqf1yONcVBFo5u0eYi0tvT4rtQCXsu+KanAardW8go4QSLw4yoED59lgV7oAhGyCalAzE7ra29j+RvvZPsQyoQuDCrtoY/TvQyMTXIXzGPDC/rKBbg=="
      }
    ],
    "uri": "/pen-test/pets",
    "args": "",
    "httpVersion": "HTTP/1.1",
    "httpMethod": "GET",
    "requestId": "GINMHHUgoAMFxug="
  }
}
```

**Example Log output for a CAPTCHA rule against a web request that doesn't have a CAPTCHA token**  
The following log listing is for a web request that matched a rule with CAPTCHA action\. The web request didn't have a CAPTCHA token, and was blocked by AWS WAF\.  

```
{
  "timestamp": 1632420416512,
  "formatVersion": 1,
  "webaclId": "arn:aws:wafv2:us-east-1:123456789012:regional/webacl/captcha-web-acl/585e38b5-afce-4d2a-b417-14fb08b66c67",
  "terminatingRuleId": "captcha-rule",
  "terminatingRuleType": "REGULAR",
  "action": "CAPTCHA",
  "terminatingRuleMatchDetails": [],
  "httpSourceName": "APIGW",
  "httpSourceId": "123456789012:b34myvfw0b:pen-test",
  "ruleGroupList": [],
  "rateBasedRuleList": [],
  "nonTerminatingMatchingRules": [],
  "requestHeadersInserted": null,
  "responseCodeSent": 405,
  "httpRequest": {
    "clientIp": "72.21.198.65",
    "country": "US",
    "headers": [
      {
        "name": "X-Forwarded-For",
        "value": "72.21.198.65"
      },
      {
        "name": "X-Forwarded-Proto",
        "value": "https"
      },
      {
        "name": "X-Forwarded-Port",
        "value": "443"
      },
      {
        "name": "Host",
        "value": "b34myvfw0b.gamma.execute-api.us-east-1.amazonaws.com"
      },
      {
        "name": "X-Amzn-Trace-Id",
        "value": "Root=1-614cc240-18b57ff33c10e5c016b508c5"
      },
      {
        "name": "sec-ch-ua",
        "value": "\"Chromium\";v=\"94\", \"Google Chrome\";v=\"94\", \";Not A Brand\";v=\"99\""
      },
      {
        "name": "sec-ch-ua-mobile",
        "value": "?0"
      },
      {
        "name": "sec-ch-ua-platform",
        "value": "\"Windows\""
      },
      {
        "name": "upgrade-insecure-requests",
        "value": "1"
      },
      {
        "name": "user-agent",
        "value": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.54 Safari/537.36"
      },
      {
        "name": "accept",
        "value": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9"
      },
      {
        "name": "sec-fetch-site",
        "value": "cross-site"
      },
      {
        "name": "sec-fetch-mode",
        "value": "navigate"
      },
      {
        "name": "sec-fetch-user",
        "value": "?1"
      },
      {
        "name": "sec-fetch-dest",
        "value": "document"
      },
      {
        "name": "accept-encoding",
        "value": "gzip, deflate, br"
      },
      {
        "name": "accept-language",
        "value": "en-US,en;q=0.9"
      }
    ],
    "uri": "/pen-test/pets",
    "args": "",
    "httpVersion": "HTTP/1.1",
    "httpMethod": "GET",
    "requestId": "GINKHEssoAMFsrg="
  },
  "captchaResponse": {
    "responseCode": 405,
    "solveTimestamp": 0,
    "failureReason": "TOKEN_MISSING"
  }
}
```