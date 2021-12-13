# Amazon CloudWatch Logs<a name="logging-cw-logs"></a>

To send logs to Amazon CloudWatch Logs, you create a CloudWatch Logs log group\. When you enable logging in AWS WAF, you provide the log group ARN\. After you enable logging for your web ACL, AWS WAF delivers logs to the CloudWatch Logs log group in log streams\. 

When you use CloudWatch Logs, you can explore the logs for your web ACL in the AWS WAF console\. In your web ACL page, select the tab **Logging insights**\. This option is in addition to the logging insights that are provided for CloudWatch Logs through the CloudWatch console\. 

Configure the log group for AWS WAF web ACL logs in the same Region as the web ACL and using the same account as you use to manage the web ACL\. For information about configuring a CloudWatch Logs log group, see [Working with Log Groups and Log Streams](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/Working-with-log-groups-and-streams.html)\.

**Quotas for log groups**  
The following default maximum quotas apply to the space and throughput allowances for CloudWatch Logs log groups\. If your logging requirements are too high for these settings, you'll see throttling metrics for `PutLogEvent` for your account\. If you see indications of throttling, you can request limit increases from both AWS WAF and CloudWatch Logs through the Service Quotas console at [Service Quotas](https://console.aws.amazon.com/servicequotas/home/services)\.
+ **Number of log streams per web ACL** – 35\. You can request an increase for this from AWS WAF\. 
+ **Throughput per log stream** – 5 MB per second\. This setting is fixed\.
+ **Throughput for all log streams for an account** – 1,500 MB per second\. You can request an increase for this from CloudWatch Logs\. 

**Log group naming**  
Your log group names must start with `aws-waf-logs-` and can end with any suffix you like, for example, `aws-waf-logs-testLogGroup2`\.

The resulting ARN format is as follows: 

```
arn:aws:logs:Region:account-id:log-group:aws-waf-logs-log-group-suffix
```

The log streams have the following naming format: 

```
Region_web-acl-name_log-stream-number
```

The log stream number is a positive integer that's less than or equal to the AWS WAF quota for the number of log streams per web ACL, as described earlier\. The quota is 35 by default\.

The following shows an example log stream for web ACL `TestWebACL` in Region `us-east-1`\. 

```
us-east-1_TestWebACL_19
```

## Permissions to publish logs to CloudWatch Logs<a name="logging-cw-logs-permissions"></a>

You must provide the following permissions settings to configure your web ACL to send logs to a CloudWatch Logs log group\. 

```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Action":[

            "wafv2:PutLoggingConfiguration",
            "wafv2:DeleteLoggingConfiguration"
         ],
         "Resource":[
            "*"
         ],
         "Effect":"Allow",
         "Sid":"LoggingConfigurationAPI"
      }
      {
         "Sid":"WebACLLoggingCWL01",
         "Action":[
            "logs:CreateLogDelivery",
            "logs:DeleteLogDelivery",
            "logs:PutResourcePolicy",
            "logs:DescribeResourcePolicies"
         ],
         "Resource":[
            "*"
         ],
         "Effect":"Allow"
      },
      {
         "Sid":"WebACLLoggingCWL02",
         "Action":[
            "logs:DescribeLogGroups"
         ],
         "Resource":[
            "CloudWatch Logs log group ARN"
         ],
         "Effect":"Allow"
      }
   ]
                }
```