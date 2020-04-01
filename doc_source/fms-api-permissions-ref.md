# Firewall Manager required permissions for API actions<a name="fms-api-permissions-ref"></a>

When you set up [Access control](fms-auth-and-access-control.md#fms-access-control) and writing permissions policies that you can attach to an IAM identity \(identity\-based policies\), use the information in this section as a guide\. For each AWS Firewall Manager API operation, you need to know the actions for which to grant permissions, and the AWS resource for which you grant the permissions\. You specify the actions in the policy's `Action` field, and you specify the resource value in the policy's `Resource` field\.

**Note**  
To specify an action, use the `fms:` prefix followed by the API operation name \(for example, `fms:CreatePolicy`\)\.  
This topic only list actions that require explicit resource permissions\. 

You can use AWS\-wide condition keys in your AWS Firewall Manager policies to express conditions\. For a complete list of AWS\-wide keys, see [Available Keys for Conditions](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\. 

To use the following Firewall Manager API actions, you need permissions on the resource: `arn:aws:fms:region:account:policy/ID`\. 
+ [DeletePolicy](https://docs.aws.amazon.com/fms/2018-01-01/APIReference/API_DeletePolicy.html)
+ [GetComplianceDetail](https://docs.aws.amazon.com/fms/2018-01-01/APIReference/API_GetComplianceDetail.html)
+ [GetPolicy](https://docs.aws.amazon.com/fms/2018-01-01/APIReference/API_GetPolicy.html)
+ [GetProtectionStatus](https://docs.aws.amazon.com/fms/2018-01-01/APIReference/API_GetProtectionStatus.html)
+ [ListComplianceStatus](https://docs.aws.amazon.com/fms/2018-01-01/APIReference/API_ListComplianceStatus.html)
+ [PutPolicy](https://docs.aws.amazon.com/fms/2018-01-01/APIReference/API_PutPolicy.html)

For more information about Firewall Manager actions and resources, see the AWS Identity and Access Management guide topic [Actions Defined by AWS Firewall Manager](https://docs.aws.amazon.com/IAM/latest/UserGuide/list_awsfirewallmanager.html#awsfirewallmanager-actions-as-permissions) 

 For the full list of the API actions available for Firewall Manager, see [AWS Firewall Manager API Reference](https://docs.aws.amazon.com/fms/2018-01-01/APIReference/)\.