# Amazon Simple Storage Service<a name="logging-s3"></a>

This topic provides information for sending your web ACL traffic logs to an Amazon S3 bucket\. 

**Note**  
You are charged for logging in addition to the charges for using AWS WAF\. For information, see [Pricing for logging web ACL traffic informationPricing for logging](logging-pricing.md)\.

To send your web ACL traffic logs to Amazon S3, you need to set up an Amazon S3 bucket for the logs\. When you enable logging in AWS WAF, you provide the bucket ARN\. For information about creating your logging bucket, see [Create a Bucket](https://docs.aws.amazon.com/AmazonS3/latest/gsg/CreatingABucket.html) in the *Amazon Simple Storage Service User Guide*\.

**Note**  
AWS WAF supports encryption with Amazon S3 buckets for key type Amazon S3 key \(SSE\-S3\) and for AWS Key Management Service \(SSE\-KMS\) AWS KMS keys\. AWS WAF doesn't support encryption for AWS Key Management Service keys that are managed by AWS\.

Your web ACLs publish their log files to the Amazon S3 bucket at 5\-minute intervals\. Each log file contains log records for the traffic recorded in the previous 5 minutes\.

The maximum file size for a log file is 75 MB\. If the log file reaches the file size limit within the 5\-minute period, the log stops adding records to it, publishes it to the Amazon S3 bucket, and then creates a new log file\.

A single log file contains interleaved entries with multiple records\. To see all the log files for a web ACL, look for entries aggregated by the web ACL name, Region, and your account ID\.

## Naming requirements and syntax<a name="logging-s3-naming"></a>

Your bucket names for AWS WAF logging must start with `aws-waf-logs-` and can end with any suffix you want\. For example, `aws-waf-logs-DOC-EXAMPLE-BUCKET-SUFFIX`\.

The bucket locations use the following syntax: 

```
s3://aws-waf-logs-DOC-EXAMPLE-BUCKET-SUFFIX/
```

The format of the bucket Amazon Resource Name \(ARN\) is as follows: 

```
arn:aws:s3:::aws-waf-logs-DOC-EXAMPLE-BUCKET-SUFFIX
```

Inside your buckets, your AWS WAF logs are written under a folder structure that's determined by your account ID, the Region, the web ACL name, and the date and time\. 

```
AWSLogs/account-id/WAFLogs/Region/web-acl-name/YYYY/MM/dd/HH/mm
```

Inside the folders, the log file names follow a similar format: 

```
account-id_waflogs_Region_web-acl-name_timestamp_hash.log.gz
```

The time specifications used in the folder structure and in the log file name adhere to the timestamp format specification `YYYYMMddTHHmmZ`\.

The following shows an example log file in an Amazon S3 bucket for a bucket named `DOC-EXAMPLE-BUCKET`\. The AWS account is `11111111111`\. The web ACL is `TEST-WEBACL` and the Region is `us-east-1`\.

```
s3://DOC-EXAMPLE-BUCKET/AWSLogs/11111111111/WAFLogs/us-east-1/TEST-WEBACL/2021/10/28/19/50/11111111111_waflogs_us-east-1_TEST-WEBACL_20211028T1950Z_e0ca43b5.log.gz
```

**Note**  
Your bucket names for AWS WAF logging must start with `aws-waf-logs-` and can end with any suffix you want\. 

## Permissions to publish logs to Amazon S3<a name="logging-s3-permissions"></a>

Configuring web ACL traffic logging for an Amazon S3 bucket requires the following permissions settings\. These permissions are set for you when you use one of the AWS WAF full access managed policies, `AWSWAFConsoleFullAccess` or `AWSWAFFullAccess`\. If you want to manage finer\-grained access to your logging and AWS WAF resources, you can set these permissions yourself\. For information about managing permissions, see [Access management for AWS resources](https://docs.aws.amazon.com/IAM/latest/UserGuide/access.html) in the *IAM User Guide*\. For information about the AWS WAF managed policies, see [AWS managed policies for AWS WAF](security-iam-awsmanpol.md)\. 

The following permissions allow you to change the web ACL logging configuration and to configure log delivery to your Amazon S3 bucket\. These permissions must be attached to the user that you use to manage AWS WAF\. 

**Note**  
When you set the permissions listed below, you might see errors in your AWS CloudTrail logs that indicate access denied, but the permissions are correct for AWS WAF logging\. 

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
      },
    {                                                                                                                                                                
       "Sid":"WebACLLogDelivery",                                                                                                                                    
       "Action":[                                                                                                                                                    
          "logs:CreateLogDelivery",                                                                                                                                  
          "logs:DeleteLogDelivery"                                                                                                                                   
       ],                                                                                                                                                            
       "Resource": "*",                                                                                                                                              
       "Effect":"Allow"                                                                                                                                              
    },  
      {
         "Sid":"WebACLLoggingS3",
         "Action":[
            "s3:PutBucketPolicy",
            "s3:GetBucketPolicy"
         ],
         "Resource": [
             "arn:aws:s3:::aws-waf-logs-example-bucket"
         ],
         "Effect":"Allow"
      }
   ]
}
```

When actions are permitted on all AWS resources, it's indicated in the policy with a `"Resource"` setting of `"*"`\. This means that the actions are permitted on all AWS resources *that each action supports*\. For example, the action `wafv2:PutLoggingConfiguration` is supported only for `wafv2` logging configuration resources\. 

By default, Amazon S3 buckets and the objects that they contain are private\. Only the bucket owner can access the bucket and the objects stored in it\. The bucket owner, however, can grant access to other resources and users by writing an access policy\.

If the user creating the log owns the bucket, the service automatically attaches the following policy to the bucket to give the log permission to publish logs to it: 

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AWSLogDeliveryWrite",
      "Effect": "Allow",
      "Principal": {
        "Service": "delivery.logs.amazonaws.com"
      },
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::aws-waf-logs-example-bucket/AWSLogs/account-id/*",
      "Condition": {
        "StringEquals": {
          "s3:x-amz-acl": "bucket-owner-full-control",
          "aws:SourceAccount": ["account-id"]
        },
        "ArnLike": {
          "aws:SourceArn": ["arn:aws:logs:region:account-id:*"]
        }
      }
    },
    {
      "Sid": "AWSLogDeliveryAclCheck",
      "Effect": "Allow",
      "Principal": {
        "Service": "delivery.logs.amazonaws.com"
      },
      "Action": "s3:GetBucketAcl",
      "Resource": "arn:aws:s3:::aws-waf-logs-example-bucket",
      "Condition": {
        "StringEquals": {
          "aws:SourceAccount": ["account-id"]
        },
        "ArnLike": {
          "aws:SourceArn": ["arn:aws:logs:region:account-id:*"]
        }
      }
    }
  ]
}
```

**Note**  
Your bucket names for AWS WAF logging must start with `aws-waf-logs-` and can end with any suffix you want\. 

If the user creating the log doesn't own the bucket, or doesn't have the `GetBucketPolicy` and `PutBucketPolicy` permissions for the bucket, the log creation fails\. In this case, the bucket owner must manually add the preceding policy to the bucket and specify the log creator's AWS account ID\. For more information, see [How Do I Add an S3 Bucket Policy?](https://docs.aws.amazon.com/AmazonS3/latest/gsg/add-bucket-policy.html) in the *Amazon Simple Storage Service User Guide*\. If the bucket receives logs from multiple accounts, add a `Resource` element entry to the `AWSLogDeliveryWrite` policy statement for each account\. 

For example, the following bucket policy allows AWS account `111122223333` to publish logs to a bucket named `aws-waf-logs-doc-example`:

```
{
    "Version": "2012-10-17",
    "Id": "AWSLogDeliveryWrite20150319",
    "Statement": [
        {
            "Sid": "AWSLogDeliveryWrite",
            "Effect": "Allow",
            "Principal": {
                "Service": "delivery.logs.amazonaws.com"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::aws-waf-logs-example-bucket/AWSLogs/111122223333/*",
            "Condition": {
                "StringEquals": {
                    "s3:x-amz-acl": "bucket-owner-full-control",
                    "aws:SourceAccount": ["111122223333"]
                },
                "ArnLike": {
                    "aws:SourceArn": ["arn:aws:logs:us-east-1:111122223333:*"]
                }
            }
        },
        {
            "Sid": "AWSLogDeliveryAclCheck",
            "Effect": "Allow",
            "Principal": {
                "Service": "delivery.logs.amazonaws.com"
            },
            "Action": "s3:GetBucketAcl",
            "Resource": "arn:aws:s3:::aws-waf-logs-example-bucket",
            "Condition": {
                "StringEquals": {
                "aws:SourceAccount": ["111122223333"]
                },
                "ArnLike": {
                "aws:SourceArn": ["arn:aws:logs:us-east-1:111122223333:*"]
                }
            }
        }
    ]
}
```

## Amazon S3 log file access<a name="logging-s3-log-file-access"></a>

In addition to the required bucket policies, Amazon S3 uses access control lists \(ACLs\) to manage access to the log files created by an AWS WAF log\. By default, the bucket owner has `FULL_CONTROL` permissions on each log file\. The log delivery owner, if different from the bucket owner, has no permissions\. The log delivery account has `READ` and `WRITE` permissions\. For more information, see [Access Control List \(ACL\) Overview](https://docs.aws.amazon.com/AmazonS3/latest/gsg/acl-overview.html) in the *Amazon Simple Storage Service User Guide*\.

The log files are compressed\. If you open the files using the Amazon S3 console, Amazon S3 decompresses the log records and displays them\. If you download the log files, you must decompress them to view the records\.