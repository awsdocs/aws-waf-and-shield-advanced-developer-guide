# How the migration works<a name="waf-migrating-how-it-works"></a>

The automated migration carries over most of your AWS WAF Classic web ACL configuration, leaving a few things that you need to handle manually\.

The following lists the high\-level steps for migrating a web ACL\. 

1. The automated migration reads everything related to your existing web ACL, without modifying or deleting anything in AWS WAF Classic\. It creates a representation of the web ACL and its related resources, compatible with AWS WAF\. It generates an AWS CloudFormation template for the new web ACL and stores it in an Amazon S3 bucket\. 

1. You deploy the template into AWS CloudFormation, in order to recreate the web ACL and related resources in AWS WAF\. 

1. You review the web ACL, and manually complete the migration, making sure that your new web ACL takes full advantage of the capabilities of the latest AWS WAF\. 

1. You manually switch your protected resources over to the new web ACL\. 