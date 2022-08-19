# Amazon CloudWatch Logs<a name="logging-cw-logs"></a>

This topic provides information for sending your web ACL traffic logs to a CloudWatch Logs log group\. 

**Note**  
You are charged for logging in addition to the charges for using AWS WAF\. For information, see [Pricing for logging web ACL traffic information](logging.md#logging-pricing)\.

To send logs to Amazon CloudWatch Logs, you create a CloudWatch Logs log group\. When you enable logging in AWS WAF, you provide the log group ARN\. After you enable logging for your web ACL, AWS WAF delivers logs to the CloudWatch Logs log group in log streams\. 

When you use CloudWatch Logs, you can explore the logs for your web ACL in the AWS WAF console\. In your web ACL page, select the tab **Logging insights**\. This option is in addition to the logging insights that are provided for CloudWatch Logs through the CloudWatch console\. 

Configure the log group for AWS WAF web ACL logs in the same Region as the web ACL and using the same account as you use to manage the web ACL\. For information about configuring a CloudWatch Logs log group, see [Working with Log Groups and Log Streams](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/Working-with-log-groups-and-streams.html)\.

## Quotas for log groups<a name="logging-cw-logs-quotas"></a>

The following default maximum quotas apply to the space and throughput allowances for CloudWatch Logs log groups\. If your logging requirements are too high for these settings, you'll see throttling metrics for `PutLogEvent` for your account\. If you see indications of throttling, you can request limit increases from both AWS WAF and CloudWatch Logs through the Service Quotas console at [Service Quotas](https://console.aws.amazon.com/servicequotas/home/services)\.
+ **Number of log streams per web ACL** – 35\. You can request an increase for this from AWS WAF\. 
+ **Throughput per log stream** – 5 MB per second\. This setting is fixed\.
+ **Throughput for all log streams for an account** – 1,500 MB per second\. You can request an increase for this from CloudWatch Logs\. 

## Log group naming<a name="logging-cw-logs-naming"></a>

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

Configuring web ACL traffic logging for a CloudWatch Logs log group requires the permissions settings described in this section\. The permissions are set for you when you use one of the AWS WAF full access managed policies, `AWSWAFConsoleFullAccess` or `AWSWAFFullAccess`\. If you want to manage finer\-grained access to your logging and AWS WAF resources, you can set the permissions yourself\. For information about managing permissions, see [Access management for AWS resources](https://docs.aws.amazon.com/IAM/latest/UserGuide/access.html) in the *IAM User Guide*\. For information about the AWS WAF managed policies, see [AWS managed policies for AWS WAF](waf-security-iam-awsmanpol.md)\. 

These permissions allow you to change the web ACL logging configuration, to configure log delivery for CloudWatch Logs, and to retrieve information about your log group\. These permissions must be attached to the user that you use to manage AWS WAF\. 

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
         "Sid":"WebACLLoggingCWL",
         "Action":[
            "logs:CreateLogDelivery",
            "logs:DeleteLogDelivery",
            "logs:PutResourcePolicy",
            "logs:DescribeResourcePolicies",
            "logs:DescribeLogGroups"
         ],
         "Resource":[
            "*"
         ],
         "Effect":"Allow"
      }
   ]
}
```

When actions are permitted on all AWS resources, it's indicated in the policy with a `"Resource"` setting of `"*"`\. This means that the actions are permitted on all AWS resources *that each action supports*\. For example, the action `wafv2:PutLoggingConfiguration` is supported only for `wafv2` logging configuration resources\. 