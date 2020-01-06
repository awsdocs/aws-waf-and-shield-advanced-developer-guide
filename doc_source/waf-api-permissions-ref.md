# AWS WAF API Permissions: Actions, Resources, and Conditions Reference<a name="waf-api-permissions-ref"></a>

When you set up [Access Control](waf-auth-and-access-control.md#access-control) and writing permissions policies that you can attach to an IAM identity \(identity\-based policies\), use the information in this section as a guide\. For each AWS WAF API operation, you need to know the actions for which you can grant permissions to perform the action, and the AWS resource for which you can grant the permissions\. You specify the actions in the policy's `Action` field, and you specify the resource value in the policy's `Resource` field\.

**Note**  
To specify an action, use the `wafv2:` prefix followed by the API operation name \(for example, `wafv2:CreateIPSet`\)\.

You can use AWS\-wide condition keys in your AWS WAF policies to express conditions\. For a complete list of AWS\-wide keys, see [Available Keys for Conditions](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\. 

**Global and regional settings**  
In the resource settings in this section, use the following `scope` and `region` settings: 
+ For CloudFront distributions, set *scope* to `global` and set *region* to `us-east-1`\.
+ For API Gateway APIs and Application Load Balancers, set *scope* to `regional` and set the *region* to the region you're interested in\.

## AWS WAF Standard API Permissions<a name="waf-api-standard-permissions"></a>

The basic CRUD and list operations on AWS resources follow a standard pattern for permissions granting\. This section shows the pattern for web ACL operations\. 

This pattern applies to web ACLs, rule groups, IP sets, and regex pattern sets\. 

**CRUD operations**
+ **AWS WAF API Operations** – [CreateWebACL](https://docs.aws.amazon.com/waf/latest/APIReference/API_CreateWebACL.html), [GetWebACL](https://docs.aws.amazon.com/waf/latest/APIReference/API_GetWebACL.html), [UpdateWebACL](https://docs.aws.amazon.com/waf/latest/APIReference/API_UpdateWebACL.html), and [DeleteWebACL](https://docs.aws.amazon.com/waf/latest/APIReference/API_DeleteWebACL.html) 
+ **API Actions** – `wafv2:CreateWebACL`, `wafv2:GetWebACL`, `wafv2:UpdateWebACL`, `wafv2:DeleteWebACL`
+ **Resources** – `arn:aws:wafv2:region:account-id:scope/webacl/entity-name/entity-ID`

**List operations**
+ **AWS WAF API Operation** – [ListWebACLs](https://docs.aws.amazon.com/waf/latest/APIReference/API_ListWebACLs.html)
+ **API Actions** – `wafv2:ListWebACLs`
+ **Resources** – `arn:aws:wafv2:region:account-id:scope/webacl/*`

  If you want to list all resources in your account, call the list operation once for global, and once for each regional application region\.

## AWS WAF Non\-Standard API Permissions<a name="waf-api-nonstandard-permissions"></a>

The following operations don't follow the standard CRUD and list pattern and require specific resource permissions settings\. 

For each operation, we list the required policy actions and their associated policy resources\. <a name="actions-related-to-objects-table_pdf"></a>

[AssociateWebACL ](https://docs.aws.amazon.com/waf/latest/APIReference/API_AssociateWebACL.html)  
**API Actions** – `wafv2:AssociateWebACL`, `elasticloadbalancing:SetWebACL`  
**Resources** –  
`arn:aws:wafv2:region:account-id:scope/webacl/entity-name/entity-ID`  
`arn:aws:elasticloadbalancing:region:account-id:loadbalancer/app/ApplicationLoadBalancerName/ApplicationLoadBalancerID`

[CheckCapacity](https://docs.aws.amazon.com/waf/latest/APIReference/API_CheckCapacity.html)  
**API Action** – `wafv2:CheckCapacity`  
**Resource** – This requires permissions on all ARNs that are referenced in the contained rules\. It doesn't require any other permissions\. 

[DescribeManagedRuleGroup](https://docs.aws.amazon.com/waf/latest/APIReference/API_DescribeManagedRuleGroup.html)  
**API Action** – `wafv2:DescribeManagedRuleGroup`  
**Resource** – `arn:aws:wafv2:region:account-id:scope/managedruleset/*`

[DisassociateWebACL](https://docs.aws.amazon.com/waf/latest/APIReference/API_DisassociateWebACL.html)  
**API Actions** – `wafv2:DisassociateWebACL`, `elasticloadbalancing:SetWebACL`  
**Resources** –  
`arn:aws:wafv2:region:account-id:scope/webacl/entity-name/entity-ID`  
 `arn:aws:elasticloadbalancing:region:account-id:loadbalancer/app/ApplicationLoadBalancerName/ApplicationLoadBalancerID`

[GetRateBasedStatementManagedKeys](https://docs.aws.amazon.com/waf/latest/APIReference/API_GetRateBasedStatementManagedKeys.html)  
**API Action** – `wafv2:GetRateBasedStatementManagedKeys`  
**Resource** – `arn:aws:wafv2:region:account-id:scope/webacl/entity-name/entity-ID`

[GetSampledRequests](https://docs.aws.amazon.com/waf/latest/APIReference/API_GetSampledRequests.html)  
**API Action** – `wafv2:GetSampledRequests`  
**Resource** – The resource permissions depend on the parameters that you specify in the API call\. You must have access to the web ACL that corresponds to the request for samples\. For example: `arn:aws:wafv2:region:account-id:scope/webacl/entity-name/entity-ID`

[ListAvailableManagedRuleGroups](https://docs.aws.amazon.com/waf/latest/APIReference/API_ListAvailableManagedRuleGroups.html)  
**API Action** – `wafv2:ListAvailableManagedRuleGroups`  
**Resource** – `arn:aws:wafv2:region:account-id:scope/managedruleset/*`