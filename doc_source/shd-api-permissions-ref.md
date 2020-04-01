# Shield required permissions for API actions<a name="shd-api-permissions-ref"></a>

When you set up [Access control](shd-auth-and-access-control.md#shd-access-control) and writing permissions policies that you can attach to an IAM identity \(identity\-based policies\), use the information in this section as a guide\. For each AWS Shield API operation, you need to know the actions for which you can grant permissions to perform the action, and the AWS resource for which you can grant the permissions\. You specify the actions in the policy's `Action` field, and you specify the resource value in the policy's `Resource` field\.

**Note**  
To specify an action, use the `shield:` prefix followed by the API operation name \(for example, `shield:CreateProtection`\)\.  
The following list only includes actions that require explicit resource permissions\.

You can use AWS\-wide condition keys in your AWS Shield policies to express conditions\. For a complete list of AWS\-wide keys, see [Available Keys for Conditions](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\. 

For each action, we list the actions and the associated policy resource specifications\. 

[AssociateDRTLogBucket](https://docs.aws.amazon.com/waf/latest/DDOSAPIReference/API_AssociateDRTLogBucket.html)  
**API Actions** – `shield:AssociateDRTLogBucket`, `s3:GetBucketPolicy`, `s3:PutBucketPolicy`  
**Resource** – `arn:aws:s3:::bucket_name/optional_object_key`

[AssociateDrtRole](https://docs.aws.amazon.com/waf/latest/DDOSAPIReference/API_AssociateDrtRole.html)  
**API Actions** – `shield:AssociateDrtRole`, `iam:GetRole`, `iam:ListAttachedRolePolicies`, `iam:PassRole`  
**Resource** – `arn:aws:iam::account-id:role/role-id`

[CreateProtection](https://docs.aws.amazon.com/waf/latest/DDOSAPIReference/API_CreateProtection.html)  
**API Actions** – `shield:CreateProtection`  
**Resource** – `arn:aws:shield::account:protection/ID`

[DeleteProtection](https://docs.aws.amazon.com/waf/latest/DDOSAPIReference/API_DeleteProtection.html)  
**API Actions** – `shield:DeleteProtection`  
**Resource** – `arn:aws:shield::account:protection/ID`

[DescribeAttack](https://docs.aws.amazon.com/waf/latest/DDOSAPIReference/API_DescribeAttack.html)  
**API Actions** – `shield:DescribeAttack`  
**Resource** – `arn:aws:shield::account:attack/ID`

[DescribeDrtAccess](https://docs.aws.amazon.com/waf/latest/DDOSAPIReference/API_DescribeDrtAccess.html)  
**API Actions** – `shield:DescribeDrtAccess`, `s3:GetBucketPolicy`  
**Resource** – `arn:aws:s3:::bucket_name/optional_object_key`

[DescribeProtection](https://docs.aws.amazon.com/waf/latest/DDOSAPIReference/API_DescribeProtection.html)  
**API Actions** – `shield:DescribeProtection`  
**Resource** – `arn:aws:shield::account:protection/ID`

[DisassociateDRTLogBucket](https://docs.aws.amazon.com/waf/latest/DDOSAPIReference/API_DisassociateDRTLogBucket.html)  
**API Actions** – `shield:DisassociateDRTLogBucket`, `s3:DeleteBucketPolicy`, `s3:GetBucketPolicy`, `s3:PutBucketPolicy`  
**Resource** – `arn:aws:s3:::bucket_name/optional_object_key`

For more information about Shield actions and resources, see the AWS Identity and Access Management guide topic [Actions Defined by AWS Shield](https://docs.aws.amazon.com/IAM/latest/UserGuide/list_awsshield.html#awsshield-actions-as-permissions)\. 

 For a full list of the API actions available for Shield, see [AWS Shield Advanced API Reference](https://docs.aws.amazon.com/waf/latest/DDOSAPIReference/)\.