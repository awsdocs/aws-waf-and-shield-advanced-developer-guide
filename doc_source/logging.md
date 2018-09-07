# Logging Web ACL Traffic Information<a name="logging"></a>

You can enable logging to get detailed information about traffic that is analyzed by your web ACL\. Information that is contained in the logs include the time that AWS WAF received the request from your AWS resource, detailed information about the request, and the action for the rule that each request matched\.

To get started, you set up an Amazon Kinesis Data Firehose\. As part of that process, you choose a destination for storing your logs\. Next, you choose the web ACL that you want to enable logging for\. After you enable logging, AWS WAF delivers logs through the firehose to your storage destination\. For more information about how to create an Amazon Kinesis Data Firehose and review the stored logs, see [What Is Amazon Kinesis Data Firehose?](https://docs.aws.amazon.com/firehose/latest/dev/what-is-this-service.html)

You must have the following permissions to successfully enable logging:
+ `iam:CreateServiceLinkedRole`
+ `firehose:ListDeliveryStreams`
+ `firehose:PutLoggingConfiguration`

For more information about service linked roles and the `iam:CreateServiceLinkedRole` permission, see [Using Service\-Linked Roles for AWS WAF](using-service-linked-roles.md)\.<a name="logging-procedure"></a>

**To enable logging for a web ACL**

1. Create an Amazon Kinesis Data Firehose using a name starting with the prefix "aws\-waf\-logs\-" For example, `aws-waf-logs-us-east-2-analytics`\. Create the data firehose with a `PUT` source and in the region that you are operating\. If you are capturing logs for Amazon CloudFront, create the firehose in US East \(N\. Virginia\)\. For more information, see [Creating an Amazon Kinesis Data Firehose Delivery Stream](https://docs.aws.amazon.com/firehose/latest/dev/basic-create.html)\.
**Note**  
One AWS WAF log is equivalent to one Kinesis Data Firehose record\. If you typically receive 10,000 requests per second and you enable full logs, you should have a 10,000 records per second limit in Kinesis Data Firehose\. For more information about Kinesis Data Firehose limits, see [Amazon Kinesis Data Firehose Limits](https://docs.aws.amazon.com/firehose/latest/dev/limits.html)\. 

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/waf/](https://console.aws.amazon.com/waf/)\. 

1. In the navigation pane, choose **Web ACLs**\.

1. Choose the web ACL that you want to enable logging for\.

1. On the **Logging** tab, choose **Enable logging**\.

1. Choose the Kinesis Data Firehose that you created in the first step\. You must choose a firehose that begins with "aws\-waf\-logs\-\."

1. \(Optional\) If you don't want certain fields and their values included in the logs, redact those fields\. Choose the field to redact, and then choose **Add**\. Repeat as necessary to redact additional fields\. The redacted fields appear as `XXX` in the logs\. For example, if you redact the **cookie** field, the **cookie** field in the logs will be `XXX`\. 

1. Choose **Enable logging**\.
**Note**  
When you successfully enable logging, AWS WAF will create a service linked role with the necessary permissions to write logs to the Amazon Kinesis Data Firehose\. For more information, see [Using Service\-Linked Roles for AWS WAF](using-service-linked-roles.md)\.<a name="logging-disable-procedure"></a>

**To disable logging for a web ACL**

1. In the navigation pane, choose **Web ACLs**\.

1. Choose the web ACL that you want to disable logging for\.

1. On the **Logging** tab, choose **Disable logging**\.

1. In the dialog box, choose **Disable logging**\.

**Example Log**  

```
{
			
	"timestamp":1533689070589,                            
	"formatVersion":1,                                   
	"webaclId":"385cb038-3a6f-4f2f-ac64-09ab912af590",  
	"terminatingRuleId":"Default_Action",                
	"terminatingRuleType":"REGULAR",                     
	"action":"ALLOW",                                    
	"httpSourceName":"CF",                               
	"httpSourceId":"i-123",                             
	"ruleGroupList":[                                    
                         {  
                          "ruleGroupId":"41f4eb08-4e1b-2985-92b5-e8abf434fad3",
                          "terminatingRule":null,    
                          "nonTerminatingMatchingRules":[                  
                                                         {“action” : “COUNT"},   
                                                         {“ruleId” : “4659b169-2083-4a91-bbd4-08851a9aaf74”}       
                                                        ]
                         }
                        ],
     
	"rateBasedRuleList":[                                 
                             {  
                              "rateBasedRuleId":"7c968ef6-32ec-4fee-96cc-51198e412e7f",   
                              "limitKey":"IP",
                              "maxRateAllowed":2000                                                                                           
                             },
                             {  
                              "rateBasedRuleId":"462b169-2083-4a93-bbd4-08851a9aaf30",
                              "limitKey":"IP",
                              "maxRateAllowed":2000
                              }
                              ],
			
	"nonTerminatingMatchingRules":[                                
                                       {“action” : “COUNT"},                                                           
                                       {“ruleId” : “4659b181-2011-4a91-bbd4-08851a9aaf52”}    
                                      ],
                                  
	"httpRequest":{                                                             
                       "clientIp":"192.10.23.23",                                           
                       "country":"US",                                                         
                       "headers":[                                                                 
                                   {  
                                    "name":"Host",
                                    "value":"127.0.0.1:1989"
                                   },
                                   {  
                                    "name":"User-Agent",
                                    "value":"curl/7.51.2"
                                   },
                                   {  
                                    "name":"Accept",
                                    "value":"*/*"
                                   }
                                 ],
                      "uri":"REDACTED",                                                
                      "args":"usernam=abc",                                         
                      "httpVersion":"HTTP/1.1",
                      "httpMethod":"GET",
                      "requestId”:”cloud front Request id”                    
                      }
}
```

Following is an explanation of each item listed in these logs\.

**timestamp**  
The timestamp in seconds\.

**formatVersion**  
The format version for the log\.

**webaclId**  
The GUID of the Web ACL\.

**terminatingRuleId**  
The ID of the rule that terminated the request\. If nothing terminates the request, the value is “Default\_Action\.”

**terminatingRuleType**  
The type of rule that terminated the request\. Possible values: RATE\_BASED, REGULAR, GROUP\.

**action**  
The action\. Possible values for a terminating rule: ALLOW, BLOCK\. COUNT would not be a terminating rule\.

**httpSourceName**  
The source of the request\. Possible values: CF,ALB \(Amazon CloudFront or an Application Load Balancer\)\.

**httpSourceId**  
The source ID\. This field will show the ID of the associated Amazon CloudFront distribution\. The ARN will be listed for application load balancers\.

**ruleGroupList**  
The list of rule groups that acted on this request\. In this sample there is only one\.

**ruleGroupId**  
The ID of the rule group\. This will be the same as terminatingRuleId if the rule blocked the request\.

**terminatingRule**  
The rule within the rule group that terminated the request\. If this is a non\-null value, it will also contain a **ruleid** and **action**\. In this case, the action will always be BLOCK\.

**nonTerminatingMatchingRules**  
The list of rules in the rule group that match the request\. These will always be "Count" rules \(non\-terminating rules that match\)\.

**action \(nonTerminatingMatchingRules group\)**  
This will be always COUNT \(which are rules that are non\-terminating and matching\)\.

**ruleId \(nonTerminatingMatchingRules group\)**  
The ID of the rule within the rule group that matches the request and was non\-terminating\. That is, COUNT rules\.

**rateBasedRuleList**  
The list of rate\-based rules that acted on the request\.

**rateBasedRuleId**  
The ID of the rate\-based rule acting on the request\. If this has terminated the request, then the ID will also be in terminatingRuleId\.

**limitKey**  
The field that AWS WAF uses to determine if requests are likely arriving from a single source and thus subject to rate monitoring\. Possible value: IP 

**maxRateAllowed**  
The maximum number of requests, which have an identical value in the field that is specified by limitKey, allowed in a five\-minute period\. If the number of requests exceeds the maxRateAllowed and the other predicates specified in the rule are also met, AWS WAF triggers the action that is specified for this rule\.

**httpRequest**  
The metadata about the request\.

**clientIp**  
The IP address of the client sending the request\.

**country**  
The source country of the request\.

**headers**  
The list of headers\.

**uri**  
The URI of the request\. This example demonstrates what the value would be if this field had been redacted\.

**args**  
The query string\.

**httpVersion**  
The HTTP version\.

**httpMethod**  
The HTTP method in the request\.

**requestId**  
The ID of the request