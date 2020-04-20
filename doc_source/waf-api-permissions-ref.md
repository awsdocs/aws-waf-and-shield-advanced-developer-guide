# AWS WAF API permissions: Actions, resources, and conditions reference<a name="waf-api-permissions-ref"></a>

When you set up [Access control](waf-auth-and-access-control.md#access-control) and writing permissions policies that you can attach to an IAM identity \(identity\-based policies\), use the information in this section as a guide\. For each AWS WAF API operation, you need to know the actions for which you can grant permissions to perform the action, and the AWS resource for which you can grant the permissions\. You specify the actions in the policy's `Action` field, and you specify the resource value in the policy's `Resource` field\.

**Note**  
To specify an action, use the `wafv2:` prefix followed by the API operation name \(for example, `wafv2:CreateIPSet`\)\.

You can use AWS\-wide condition keys in your AWS WAF policies to express conditions\. For a complete list of AWS\-wide keys, see [Available Keys for Conditions](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\. 

**Global and regional settings**  
In the resource settings in this section, use the following `scope` and `region` settings: 
+ For CloudFront distributions, set *scope* to `global` and set *region* to `us-east-1`\.
+ For API Gateway APIs and Application Load Balancers, set *scope* to `regional` and set the *region* to the region you're interested in\.

## AWS WAF API permissions for references to resources<a name="waf-api-permissions-for-refs"></a>

For all resource permissions settings, if a resource references any other resource by Amazon resource name \(ARN\), you must have permissions to access the referenced resources, in addition to the permission required to access the first resource\. For example, to work with a web ACL that references an IP set, regex pattern set, or rule group, you need to have access to the IP set, regex pattern set, or rule group resource in addition to having access to the web ACL resource\. 

## AWS WAF standard API permissions<a name="waf-api-standard-permissions"></a>

The basic CRUD and list operations on AWS resources follow a standard pattern for permissions granting\. The pattern applies to web ACLs, rule groups, IP sets, and regex pattern sets\. 

**To grant permissions for Web ACLs**  
Apply the permissions for the web ACL and for any resource the web ACL references: 
+ Use the CRUD and list operations permissions guidance in this section for `WebACL` and `webacl`\. 
+ For any rule groups that the web ACL references, use the guidance in this section with `RuleGroup` and `rulegroup`\.
+ For any managed rule groups that the web ACL references, provide the permissions for `DescribeManagedRuleGroup`, listed under [AWS WAF non\-standard API and required permissions for actions](#waf-api-nonstandard-permissions)\.
+ For any IP sets that the web ACL references, use the guidance in this section with `IPSet` and `ipset`\.
+ For any regex pattern sets that the web ACL references, use the guidance in this section with `RegexPatternSet` and `regexpatternset`\.

**To grant permissions for rule groups**  
Apply the permissions for the rule group and for any resource the rule group references: 
+ Use the CRUD and list operations permissions guidance in this section with `RuleGroup` and `rulegroup`\. 
+ For any IP sets that the rule group references, use the guidance in this section with `IPSet` and `ipset`\.
+ For any regex pattern sets that the rule group references, use the guidance in this section with `RegexPatternSet` and `regexpatternset`\.

**To grant permissions for IP sets**  
For IP sets, use the CRUD and list operations permissions guidance in this section with `IPSet` and `ipset`\.

**To grant permissions for regex pattern sets**  
For regex pattern sets, use the CRUD and list operations permissions guidance in this section with `RegexPatternSet` and `regexpatternset`\.

### AWS WAF CRUD and List permissions<a name="waf-crud-list-permissions"></a>

The patterns for CRUD and list apply to web ACLs, rule groups, IP sets, and regex pattern sets\. This section shows the pattern for web ACL operations\. For other resource types, substitute in the strings for those, according to the guidance preceding this section\.

**CRUD operations for web ACL**
+ **AWS WAF API Operations** – [CreateWebACL](https://docs.aws.amazon.com/waf/latest/APIReference/API_CreateWebACL.html), [GetWebACL](https://docs.aws.amazon.com/waf/latest/APIReference/API_GetWebACL.html), [UpdateWebACL](https://docs.aws.amazon.com/waf/latest/APIReference/API_UpdateWebACL.html), and [DeleteWebACL](https://docs.aws.amazon.com/waf/latest/APIReference/API_DeleteWebACL.html) 
+ **API Actions** – `wafv2:CreateWebACL`, `wafv2:GetWebACL`, `wafv2:UpdateWebACL`, `wafv2:DeleteWebACL`
+ **Resources** – `arn:aws:wafv2:region:account-id:scope/webacl/entity-name/entity-ID` 

**List operations for web ACL**
+ **AWS WAF API Operation** – [ListWebACLs](https://docs.aws.amazon.com/waf/latest/APIReference/API_ListWebACLs.html)
+ **API Actions** – `wafv2:ListWebACLs`
+ **Resources** – `arn:aws:wafv2:region:account-id:scope/webacl/*`

  If you want to list all resources in your account, call the list operation once for global, and once for each regional application region\.

## AWS WAF non\-standard API permissions<a name="waf-api-nonstandard-permissions"></a>

The following operations don't follow the standard CRUD and list pattern and require specific resource permissions settings\. 

For each operation, we list the required policy actions and their associated policy resources\. <a name="actions-related-to-objects-table_pdf"></a>

[AssociateWebACL ](https://docs.aws.amazon.com/waf/latest/APIReference/API_AssociateWebACL.html)  
**API Actions** – `wafv2:AssociateWebACL`, `elasticloadbalancing:SetWebACL`, `apigateway:SetWebACL`  
**Resources** –  
`arn:aws:wafv2:region:account-id:scope/webacl/entity-name/entity-ID`  
`arn:aws:elasticloadbalancing:region:account-id:loadbalancer/app/ApplicationLoadBalancerName/ApplicationLoadBalancerID`  
`arn:aws:apigateway:region::/restapis/api-ID/stages/stage-name`

[CheckCapacity](https://docs.aws.amazon.com/waf/latest/APIReference/API_CheckCapacity.html)  
**API Action** – `wafv2:CheckCapacity`  
**Resource** – This requires permissions on all ARNs that are referenced in the contained rules\. It doesn't require any other permissions\. 

[DescribeManagedRuleGroup](https://docs.aws.amazon.com/waf/latest/APIReference/API_DescribeManagedRuleGroup.html)  
**API Action** – `wafv2:DescribeManagedRuleGroup`  
**Resource** – `arn:aws:wafv2:region:account-id:scope/managedruleset/*`

[DisassociateWebACL](https://docs.aws.amazon.com/waf/latest/APIReference/API_DisassociateWebACL.html)  
**API Actions** – `wafv2:DisassociateWebACL`, `elasticloadbalancing:SetWebACL`, `apigateway:SetWebACL`  
**Resources** –  
`arn:aws:wafv2:region:account-id:scope/webacl/entity-name/entity-ID`  
 `arn:aws:elasticloadbalancing:region:account-id:loadbalancer/app/ApplicationLoadBalancerName/ApplicationLoadBalancerID`  
`arn:aws:apigateway:region::/restapis/api-ID/stages/stage-name`

[GetRateBasedStatementManagedKeys](https://docs.aws.amazon.com/waf/latest/APIReference/API_GetRateBasedStatementManagedKeys.html)  
**API Action** – `wafv2:GetRateBasedStatementManagedKeys`  
**Resource** – `arn:aws:wafv2:region:account-id:scope/webacl/entity-name/entity-ID`

[GetSampledRequests](https://docs.aws.amazon.com/waf/latest/APIReference/API_GetSampledRequests.html)  
**API Action** – `wafv2:GetSampledRequests`  
**Resource** – The resource permissions depend on the parameters that you specify in the API call\. You must have access to the web ACL that corresponds to the request for samples\. For example: `arn:aws:wafv2:region:account-id:scope/webacl/entity-name/entity-ID`

[ListAvailableManagedRuleGroups](https://docs.aws.amazon.com/waf/latest/APIReference/API_ListAvailableManagedRuleGroups.html)  
**API Action** – `wafv2:ListAvailableManagedRuleGroups`  
**Resource** – `arn:aws:wafv2:region:account-id:scope/managedruleset/*`