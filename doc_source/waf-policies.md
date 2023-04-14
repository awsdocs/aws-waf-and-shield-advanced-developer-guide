# AWS WAF policies<a name="waf-policies"></a>

In a Firewall Manager AWS WAF policy, you specify the AWS WAF rule groups that you want to use across your resources\. When you apply the policy, in each account that's within policy scope, Firewall Manager creates a web ACL that's managed by Firewall Manager\. In the resulting web ACLs, individual account managers can add rules and rule groups, in addition to the rule groups that you defined through Firewall Manager\. 

When Firewall Manager creates a web ACL for the policy, it names the web ACL `FMManagedWebACLV2-policy name-timestamp`\. The timestamp is in UTC milliseconds\. For example, `FMManagedWebACLV2-MyWAFPolicyName-1621880374078`\.

AWS Firewall Manager enables sampling and Amazon CloudWatch metrics for the web ACLs and rule groups that it creates for an AWS WAF policy\. 

**Note**  
If a resource configured with [advanced automatic application layer DDoS mitigation](ddos-automatic-app-layer-response.md) comes into scope of a AWS WAF policy, Firewall Manager will be unable to associate the web ACL created by the AWS WAF policy to the resource\.>

## Rule groups in AWS WAF policies<a name="waf-policies-rule-groups"></a>

The web ACLs that are managed by Firewall Manager AWS WAF policies contain three sets of rules\. These sets provide a higher level of prioritization for the rules and rule groups in the web ACL: 
+ First rule groups, defined by you in the Firewall Manager AWS WAF policy\. AWS WAF evaluates these rule groups first\.
+ Rules and rule groups that are defined by the account managers in the web ACLs\. AWS WAF evaluates any account\-managed rules or rule groups next\. 
+ Last rule groups, defined by you in the Firewall Manager AWS WAF policy\. AWS WAF evaluates these rule groups last\.

Within each of these sets of rules, AWS WAF evaluates rules and rule groups as usual, according to their priority settings within the set\.

In the policy's first and last rule groups sets, you can only add rule groups\. You can use managed rule groups, which AWS Managed Rules and AWS Marketplace sellers create and maintain for you\. You can also manage and use your own rule groups\. For more information about all of these options, see [Rule groups](waf-rule-groups.md)\.

If you want to use your own rule groups, you create those before you create your Firewall Manager AWS WAF policy\. For guidance, see [Managing your own rule groups](waf-user-created-rule-groups.md)\. To use an individual custom rule, you must define your own rule group, define your rule within that, and then use the rule group in your policy\.

The first and last AWS WAF rule groups that you manage through Firewall Manager have names that begin with `PREFMManaged-` or `POSTFMManaged-`, respectively, followed by the Firewall Manager policy name, and the rule group creation timestamp, in UTC milliseconds\. For example, `PREFMManaged-MyWAFPolicyName-1621880555123`\.

For information about how AWS WAF evaluates web requests, see [Web ACL rule and rule group evaluation](web-acl-processing.md)\.

For the procedure to create a Firewall Manager AWS WAF policy, see [Creating an AWS Firewall Manager policy for AWS WAF](create-policy.md#creating-firewall-manager-policy-for-waf)\.

Firewall Manager enables sampling and Amazon CloudWatch metrics for the rule groups that you define for the AWS WAF policy\. 

Individual account owners have complete control over the metrics and sampling configuration for any rule or rule group that they add to the policy's managed web ACLs\. 

### Limitations<a name="waf-policies-rule-groups-limitations"></a>

Note the following limitations when working with rule groups in AWS WAF policies\.
+ Firewall Manager supports AWS WAF Bot Control rule groups, with the following exceptions:
  + The Bot Control targeted protecion level isn't supported\.
  + Only the `COUNT` rule action override is supported\. Other rule action override types aren't currently supported\.

  For information about Bot Control in AWS WAF, see [AWS WAF Bot Control](waf-bot-control.md)\.

## Configuring logging for an AWS WAF policy<a name="waf-policies-logging-config"></a>

You can enable centralized logging for your AWS WAF policies to get detailed information about traffic that's analyzed by your web ACL within your organization\. Information in the logs includes the time that AWS WAF received the request from your AWS resource, detailed information about the request, and the action for the rule that each request matched from all in\-scope accounts\. You can send your logs to an Amazon Kinesis Data Firehose data stream or Amazon Simple Storage Service \(S3\) bucket\. For information about AWS WAF logging, see [Logging web ACL traffic](logging.md) in the *AWS WAF Developer Guide*\.

**Note**  
AWS Firewall Manager supports this option for AWS WAFV2, not for AWS WAF Classic\.

**Topics**
+ [Logging destinations](#waf-policies-logging-destinations)
+ [Enabling logging](#waf-policies-enabling-logging)
+ [Disabling logging](#waf-policies-disabling-logging)

### Logging destinations<a name="waf-policies-logging-destinations"></a>

This section describes the logging destinations that you can choose to send your AWS WAF policy logs\. Each section provides guidance for configuring logging for the destination type and information about any behavior that's specific to the destination type\. After you've configured your logging destination, you can provide its specifications to your Firewall Manager AWS WAF policy to start logging to it\.

**Note**  
Firewall Manager doesn't modify any existing logging configurations in your organization's member accounts\. 

#### Amazon Kinesis Data Firehose data streams<a name="waf-policies-logging-destinations-kinesis-data-firehose"></a>

This topic provides information for sending your web ACL traffic logs to an Amazon Kinesis Data Firehose data stream\.

When you enable Amazon Kinesis Data Firehose logging, Firewall Manager sends logs from your policy's web ACLs to an Amazon Kinesis Data Firehose where you've configured a storage destination\. After you enable logging, AWS WAF delivers logs for each configured web ACL, through the HTTPS endpoint of Kinesis Data Firehose to the configured storage destination\. Before you use it, test your delivery stream to be sure that it has enough throughput to accommodate your organization's logs\. For more information about how to create an Amazon Kinesis Data Firehose and review the stored logs, see [What Is Amazon Kinesis Data Firehose?](https://docs.aws.amazon.com/firehose/latest/dev/what-is-this-service.html)

You must have the following permissions to successfully enable logging with a Kinesis:
+ `iam:CreateServiceLinkedRole`
+ `firehose:ListDeliveryStreams`
+ `wafv2:PutLoggingConfiguration`

When you configure a Amazon Kinesis Data Firehose logging destination on an AWS WAF policy, Firewall Manager creates a web ACL for the policy in the Firewall Manager administrator account as follows: 
+ Firewall Manager creates the web ACL in the Firewall Manager administrator account regardless of whether the account is in scope of the policy\.
+ The web ACL has logging enabled, with a log name `FMManagedWebACLV2-Loggingpolicy name-timestamp`, where the timestamp is the UTC time that the log was enabled for the web ACL, in milliseconds\. For example, `FMManagedWebACLV2-LoggingMyWAFPolicyName-1621880565180`\. The web ACL has no rule groups and no associated resources\. 
+ You are charged for the web ACL according to the AWS WAF pricing guidelines\. For more information, see [AWS WAF Pricing](http://aws.amazon.com/waf/pricing/)\. 
+ Firewall Manager deletes the web ACL when you delete the policy\. 

For information about service\-linked roles and the `iam:CreateServiceLinkedRole` permission, see [Using service\-linked roles for AWS WAF](using-service-linked-roles.md)\.

For more information about creating your delivery stream, see [Creating an Amazon Kinesis Data Firehose Delivery Stream](https://docs.aws.amazon.com/firehose/latest/dev/basic-create.html)\.

#### Amazon Simple Storage Service buckets<a name="waf-policies-logging-destinations-s3"></a>

This topic provides information for sending your web ACL traffic logs to an Amazon S3 bucket\.

For information about the requirements for creating your Amazon S3 bucket for logging and budket naming requirements, see [Amazon Simple Storage Service ](https://docs.aws.amazon.com/waf/latest/developerguide/logging-s3.html) in the *AWS WAF Developer Guide*\.

**Eventual consistency**  
When you make change to AWS WAF policies configured with an Amazon S3 logging destination, Firewall Manager updates the bucket policy to add the permissions necessary for logging\. When doing so, Firewall Manager follows the last\-writer\-wins semantics and data consistency models that Amazon Simple Storage Service follows\. If you concurrently make multiple policy updates to a Amazon S3 destination in the Firewall Manager console or through the [PutPolicy](https://docs.aws.amazon.com/fms/2018-01-01/APIReference/API_PutPolicy.html) API, some permissions may not be saved\. For more information about the Amazon S3 data consistency model, see [Amazon S3 data consistency model](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html#ConsistencyModel) in the *Amazon Simple Storage Service User Guide*\.

##### Permissions to publish logs to an Amazon S3 bucket<a name="waf-policies-logging-s3-permissions"></a>

Configuring web ACL traffic logging for an Amazon S3 bucket in a AWS WAF policy requires the following permissions settings\. Firewall Manager automatically attaches these permissions to your Amazon S3 bucket when you configure Amazon S3 as your logging destination to give the service permission to publish logs to the bucket\. If you want to manage finer\-grained access to your logging and Firewall Manager resources, you can set these permissions yourself\. For information about managing permissions, see [Access management for AWS resources](https://docs.aws.amazon.com/IAM/latest/UserGuide/access.html) in the *IAM User Guide*\. For information about the AWS WAF managed policies, see [AWS managed policies for AWS WAF](security-iam-awsmanpol.md)\. 

```
{
    "Version": "2012-10-17",
    "Id": "AWSLogDeliveryForFirewallManager",
    "Statement": [
        {
            "Sid": "AWSLogDeliveryAclCheckFMS",
            "Effect": "Allow",
            "Principal": {
                "Service": "delivery.logs.amazonaws.com"
            },
            "Action": "s3:GetBucketAcl",
            "Resource": "arn:aws:s3:::aws-waf-example-bucket"
        },
        {
            "Sid": "AWSLogDeliveryWriteFMS",
            "Effect": "Allow",
            "Principal": {
                "Service": "delivery.logs.amazonaws.com"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::aws-waf-logs-example-bucket/policy-id/AWSLogs/*",
            "Condition": {
                "StringEquals": {
                    "s3:x-amz-acl": "bucket-owner-full-control"
                }
            }
        }
    ]
}
```

To prevent the cross\-service confused deputy problem, you can add the [https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourcearn](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourcearn) and [https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourceaccount](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourceaccount) global condition context keys to your bucket's policy\. To add these keys, you can either modify the policy that Firewall Manager creates for you when you configure the logging destination, or if you want fine grained control, you can create your own policy\. If you add these conditions to your logging destination policy, Firewall Manager won't validate or monitor the confused deputy protections\. For general information about the confused deputy problem, see [The confused deputy problem ](https://docs.aws.amazon.com/IAM/latest/UserGuide/confused-deputy.html) in the *IAM User Guide*\. 

When you add the `sourceAccount` add `sourceArn` properties it'll increase the bucket policy size\. If you're adding a long list of `sourceAccount` add `sourceArn` properties, take care not to exceed the Amazon S3 [bucket policy size](https://docs.aws.amazon.com/general/latest/gr/s3.html#limits_s3) quota\.

The following example shows how to prevent the confused deputy problem by using the `aws:SourceArn` and `aws:SourceAccount` global condition context keys in your bucket's policy\. Replace *member\-account\-id* with the account IDs of the members in your organization\.

```
{
   "Version":"2012-10-17",
   "Id":"AWSLogDeliveryForFirewallManager",
   "Statement":[
      {
         "Sid":"AWSLogDeliveryAclCheckFMS",
         "Effect":"Allow",
         "Principal":{
            "Service":"delivery.logs.amazonaws.com"
         },
         "Action":"s3:GetBucketAcl",
         "Resource":"arn:aws:s3:::aws-waf-logs-example-bucket",
         "Condition":{
            "StringEquals":{
               "aws:SourceAccount":[
                  "member-account-id",
                  "member-account-id"
               ]
            },
            "ArnLike":{
               "aws:SourceArn":[
                  "arn:aws:logs:*:member-account-id:*",
                  "arn:aws:logs:*:member-account-id:*"
               ]
            }
         }
      },
      {
         "Sid":"AWSLogDeliveryWriteFMS",
         "Effect":"Allow",
         "Principal":{
            "Service":"delivery.logs.amazonaws.com"
         },
         "Action":"s3:PutObject",
         "Resource":"arn:aws:s3:::aws-waf-logs-example-bucket/policy-id/AWSLogs/*",
         "Condition":{
            "StringEquals":{
               "s3:x-amz-acl":"bucket-owner-full-control",
               "aws:SourceAccount":[
                    "member-account-id",
                  "member-account-id"
               ]
            },
            "ArnLike":{
               "aws:SourceArn":[
                  "arn:aws:logs:*:member-account-id-1:*",
                  "arn:aws:logs:*:member-account-id-2:*"
               ]
            }
         }
      }
   ]
}
```

##### Server\-side encryption<a name="waf-policies-logging-s3-kms-permissions"></a>

You can enable Amazon S3 server\-side encryption or use a AWS Key Management Service customer managed key on your S3 bucket\. If you choose to use the default Amazon S3 encryption on your Amazon S3 bucket for AWS WAF logs, you don't need to take any special action\. However, if you choose to use a customer\-provided encryption key to encrypt your Amazon S3 data at rest, you must add the following permission statement to your AWS Key Management Service key policy:

```
{
            "Sid": "Allow Logs Delivery to use the key",
            "Effect": "Allow",
            "Principal": {
                "Service": "delivery.logs.amazonaws.com"
            },
            "Action": [
                "kms:Encrypt",
                "kms:Decrypt",
                "kms:ReEncrypt*",
                "kms:GenerateDataKey*",
                "kms:DescribeKey"
            ],
            "Resource": "*"
}
```

For information about using customer\-provided encryption keys with Amazon S3, see [Using server\-side encryption with customer\-provided keys \(SSE\-C\)](https://docs.aws.amazon.com/AmazonS3/latest/userguide/ServerSideEncryptionCustomerKeys.html) in the *Amazon Simple Storage Service User Guide*\.

### Enabling logging<a name="waf-policies-enabling-logging"></a>

The following procedure describes how to enable logging for a AWS WAF policy in the Firewall Manager console\.

**To enable logging for an AWS WAF policy**

1. Before you can enable logging, you must configure your logging destination resources as the following:
   + **Amazon Kinesis Data Streams** \- Create an Amazon Kinesis Data Firehose using your Firewall Manager administrator account\. Use a name starting with the prefix `aws-waf-logs-`\. For example, `aws-waf-logs-firewall-manager-central`\. Create the data firehose with a `PUT` source and in the Region that you are operating\. If you are capturing logs for Amazon CloudFront, create the firehose in US East \(N\. Virginia\)\. Before you use it, test your delivery stream to be sure that it has enough throughput to accommodate your organization's logs\. For more information, see [Creating an Amazon Kinesis Data Firehose delivery stream](https://docs.aws.amazon.com/firehose/latest/dev/basic-create.html)\.
   + **Amazon Simple Storage Service buckets** \- Create an Amazon S3 bucket according to the guidelines in the [Amazon Simple Storage Service ](https://docs.aws.amazon.com/waf/latest/developerguide/logging-s3.html) topic in the *AWS WAF Developer Guide*\. You must also configure your Amazon S3 bucket with the permissions listed in [Permissions to publish logs to an Amazon S3 bucket ](#waf-policies-logging-s3-permissions)\.

1. Sign in to the AWS Management Console using your Firewall Manager administrator account, and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fmsv2](https://console.aws.amazon.com/wafv2/fmsv2)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [AWS Firewall Manager prerequisites](fms-prereq.md)\.

1. In the navigation pane, choose **Security Policies**\.

1. Choose the AWS WAF policy that you want to enable logging for\. For more information about AWS WAF logging, see [Logging web ACL traffic](logging.md)\.

1. On the **Policy details** tab, in the **Policy rules** section, choose **Edit**\. 

1. For **Logging configuration**, choose **Enable logging** to turn on logging\. Logging provides detailed information about traffic that is analyzed by your web ACL\. Choose the **Logging destination**, and then choose the logging destination that you configured\. You must choose a logging destination whose name begins with `aws-waf-logs-`\. For information about configuring a AWS WAF logging destination, see [Configuring logging for an AWS WAF policy](#waf-policies-logging-config)\.

1. \(Optional\) If you don't want certain fields and their values included in the logs, redact those fields\. Choose the field to redact, and then choose **Add**\. Repeat as necessary to redact additional fields\. The redacted fields appear as `REDACTED` in the logs\. For example, if you redact the **URI** field, the **URI** field in the logs will be `REDACTED`\. 

1. \(Optional\) If you don't want to send all requests to the logs, add your filtering criteria and behavior\. Under **Filter logs**, for each filter that you want to apply, choose **Add filter**, then choose your filtering criteria and specify whether you want to keep or drop requests that match the criteria\. When you finish adding filters, if needed, modify the **Default logging behavior**\. For more information, see [Managing logging for a web ACL](logging-management.md) in the *AWS WAF Developer Guide*\.

1. Choose **Next**\.

1. Review your settings, then choose **Save** to save your changes to the policy\.

### Disabling logging<a name="waf-policies-disabling-logging"></a>

The following procedure describes how to disable logging for a AWS WAF policy in the Firewall Manager console\.

**To disable logging for an AWS WAF policy**

1. Sign in to the AWS Management Console using your Firewall Manager administrator account, and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fmsv2](https://console.aws.amazon.com/wafv2/fmsv2)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [AWS Firewall Manager prerequisites](fms-prereq.md)\.

1. In the navigation pane, choose **Security Policies**\.

1. Choose the AWS WAF policy that you want to disable logging for\.

1. On the **Policy details** tab, in the **Policy rules** section, choose **Edit**\. 

1. For **Logging configuration status**, choose **Disabled**\.

1. Choose **Next**\.

1. Review your settings, then choose **Save** to save your changes to the policy\.