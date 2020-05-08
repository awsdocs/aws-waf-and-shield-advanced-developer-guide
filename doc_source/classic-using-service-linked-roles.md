# Using service\-linked roles for AWS WAF Classic<a name="classic-using-service-linked-roles"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

AWS WAF Classic uses AWS Identity and Access Management \(IAM\)[ service\-linked roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-linked-role)\. A service\-linked role is a unique type of IAM role that is linked directly to AWS WAF Classic\. Service\-linked roles are predefined by AWS WAF Classic and include all the permissions that the service requires to call other AWS services on your behalf\. 

A service\-linked role makes setting up AWS WAF Classic easier because you don’t have to manually add the necessary permissions\. AWS WAF Classic defines the permissions of its service\-linked roles, and unless defined otherwise, only AWS WAF Classic can assume its roles\. The defined permissions include the trust policy and the permissions policy\. That permissions policy can't be attached to any other IAM entity\.

You can delete a service\-linked role only after first deleting the role's related resources\. This protects your AWS WAF Classic resources because you can't inadvertently remove permission to access the resources\.

For information about other services that support service\-linked roles, see [AWS Services That Work with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html) and look for the services that have **Yes **in the **Service\-Linked Role** column\. Choose a **Yes** with a link to view the service\-linked role documentation for that service\.

## Service\-linked role permissions for AWS WAF Classic<a name="classic-slr-permissions"></a>

AWS WAF Classic uses the following service\-linked roles:
+ `AWSServiceRoleForWAFLogging`
+ `AWSServiceRoleForWAFRegionalLogging`

AWS WAF Classic uses these service\-linked roles to write logs to Amazon Kinesis Data Firehose\. These roles are used only if you enable logging in AWS WAF\. For more information, see [Logging Web ACL traffic information](classic-logging.md)\.

The `AWSServiceRoleForWAFLogging` and `AWSServiceRoleForWAFRegionalLogging` service\-linked roles trust the following services \(respectively\) to assume the role:
+ `waf.amazonaws.com`

  `waf-regional.amazonaws.com`

The permissions policies of the roles allow AWS WAF Classic to complete the following actions on the specified resources:
+ Action: `firehose:PutRecord` and `firehose:PutRecordBatch` on Amazon Kinesis Data Firehose data stream resources with a name that starts with "aws\-waf\-logs\-\." For example, `aws-waf-logs-us-east-2-analytics`\.

You must configure permissions to allow an IAM entity \(such as a user, group, or role\) to create, edit, or delete a service\-linked role\. For more information, see [Service\-Linked Role Permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#service-linked-role-permissions) in the *IAM User Guide*\.

## Creating a service\-linked role for AWS WAF Classic<a name="classic-create-slr"></a>

You don't need to manually create a service\-linked role\. When you enable AWS WAF Classic logging on the AWS Management Console, or you make a `PutLoggingConfiguration` request in the AWS WAF Classic CLI or the AWS WAF Classic API, AWS WAF Classic creates the service\-linked role for you\. 

You must have the `iam:CreateServiceLinkedRole` permission to enable logging\.

If you delete this service\-linked role, and then need to create it again, you can use the same process to recreate the role in your account\. When you enable AWS WAF Classic logging, AWS WAF Classic creates the service\-linked role for you again\. 

## Editing a service\-linked role for AWS WAF Classic<a name="classic-edit-slr"></a>

AWS WAF Classic doesn't allow you to edit the `AWSServiceRoleForWAFLogging` and `AWSServiceRoleForWAFRegionalLogging` service\-linked roles\. After you create a service\-linked role, you can't change the name of the role because various entities might reference the role\. However, you can edit the description of the role using IAM\. For more information, see [Editing a Service\-Linked Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#edit-service-linked-role) in the *IAM User Guide*\.

## Deleting a service\-linked role for AWS WAF Classic<a name="classic-delete-slr"></a>

If you no longer need to use a feature or service that requires a service\-linked role, we recommend that you delete that role\. That way you don’t have an unused entity that is not actively monitored or maintained\. However, you must clean up the resources for your service\-linked role before you can manually delete it\.

**Note**  
If the AWS WAF Classic service is using the role when you try to delete the resources, then the deletion might fail\. If that happens, wait for a few minutes and try the operation again\.

**To delete AWS WAF Classic resources used by the `AWSServiceRoleForWAFLogging` and `AWSServiceRoleForWAFRegionalLogging`**

1. On the AWS WAF Classic console, remove logging from every web ACL\. For more information, see [Logging Web ACL traffic information](classic-logging.md)\.

1. Using the API or CLI, submit a `DeleteLoggingConfiguration` request for each web ACL that has logging enabled\. For more information, see [AWS WAF Classic API Reference](https://docs.aws.amazon.com/waf/latest/APIReference/Welcome.html)\.

**To manually delete the service\-linked role using IAM**

Use the IAM console, the IAM CLI, or the IAM API to delete the `AWSServiceRoleForWAFLogging` and `AWSServiceRoleForWAFRegionalLogging` service\-linked roles\. For more information, see [Deleting a Service\-Linked Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#delete-service-linked-role) in the *IAM User Guide*\.

## Supported Regions for AWS WAF Classic service\-linked roles<a name="classic-slr-regions"></a>

AWS WAF Classic supports using service\-linked roles in the following AWS Regions\.


****  

| Region Name | Region Identity | Support in AWS WAF Classic | 
| --- | --- | --- | 
| US East \(N\. Virginia\) | us\-east\-1 | Yes | 
| US East \(Ohio\) | us\-east\-2 | Yes | 
| US West \(N\. California\) | us\-west\-1 | Yes | 
| US West \(Oregon\) | us\-west\-2 | Yes | 
| Asia Pacific \(Mumbai\) | ap\-south\-1 | Yes | 
| Asia Pacific \(Osaka\-Local\) | ap\-northeast\-3 | Yes | 
| Asia Pacific \(Seoul\) | ap\-northeast\-2 | Yes | 
| Asia Pacific \(Singapore\) | ap\-southeast\-1 | Yes | 
| Asia Pacific \(Sydney\) | ap\-southeast\-2 | Yes | 
| Asia Pacific \(Tokyo\) | ap\-northeast\-1 | Yes | 
| Canada \(Central\) | ca\-central\-1 | Yes | 
| Europe \(Frankfurt\) | eu\-central\-1 | Yes | 
| Europe \(Ireland\) | eu\-west\-1 | Yes | 
| Europe \(London\) | eu\-west\-2 | Yes | 
| Europe \(Paris\) | eu\-west\-3 | Yes | 
| South America \(São Paulo\) | sa\-east\-1 | Yes | 