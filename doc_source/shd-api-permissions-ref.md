# Shield Advanced required permissions for API actions<a name="shd-api-permissions-ref"></a>

When you set up [Access control](shd-auth-and-access-control.md#shd-access-control) and writing permissions policies that you can attach to an IAM identity \(identity\-based policies\), use the information in this section as a guide\. For each AWS Shield Advanced API operation, you need to know the actions for which you can grant permissions to perform the action, and the AWS resource for which you can grant the permissions\. You specify the actions in the policy's `Action` field, and you specify the resource value in the policy's `Resource` field\.

**Note**  
To specify an action, use the `shield:` prefix followed by the API operation name \(for example, `shield:CreateProtection`\)\.

You can use AWS condition keys in your AWS Shield Advanced policies to express conditions\. For a complete list of AWS keys, see [Available Keys for Conditions](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\. 

To see Shield Advanced actions, resource types, and condition keys, see [Actions, resources, and condition keys for AWS Shield Advanced](https://docs.aws.amazon.com/service-authorization/latest/reference/list_awsshield.html) in the *Service Authorization Reference*\.

For more information about Shield actions and resources, see the AWS Identity and Access Management guide topic [Actions Defined by AWS Shield](https://docs.aws.amazon.com/IAM/latest/UserGuide/list_awsshield.html#awsshield-actions-as-permissions)\. 

 For a full list of the API actions available for Shield, see [AWS Shield Advanced API Reference](https://docs.aws.amazon.com/waf/latest/DDOSAPIReference/)\.