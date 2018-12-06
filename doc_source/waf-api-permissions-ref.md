# AWS WAF API Permissions: Actions, Resources, and Conditions Reference<a name="waf-api-permissions-ref"></a>

When you are setting up [Access Control](waf-auth-and-access-control.md#access-control) and writing permissions policies that you can attach to an IAM identity \(identity\-based policies\), you can use the following table as a reference\. The table lists each AWS WAF API operation, the corresponding actions for which you can grant permissions to perform the action, and the AWS resource for which you can grant the permissions\. You specify the actions in the policy's `Action` field, and you specify the resource value in the policy's `Resource` field\. 

You can use AWS\-wide condition keys in your AWS WAF policies to express conditions\. For a complete list of AWS\-wide keys, see [Available Keys for Conditions](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\. 

**Note**  
To specify an action, use the `waf:` prefix followed by the API operation name \(for example, `waf:CreateIPSet`\)\.