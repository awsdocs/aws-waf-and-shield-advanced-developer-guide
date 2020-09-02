# Overview of managing access permissions to your AWS WAF resources<a name="access-control-overview"></a>

Every AWS resource is owned by an AWS account, and permissions to create or access a resource are governed by permissions policies\. An account administrator can attach permissions policies to IAM identities \(that is, users, groups, and roles\)\. Some services also support attaching permissions policies to resources\.

**Note**  
An *account administrator* \(or administrator user\) is a user with administrator privileges\. For more information, see [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) in the *IAM User Guide*\.

When granting permissions, you decide who is getting the permissions, the resources they get permissions for, and the specific operations that you want to allow on those resources\.

## Topics<a name="topics1"></a>
+ [AWS WAF resources and operations](#access-control-resources)
+ [Understanding resource ownership](#access-control-resource-ownership)
+  [Managing access to resources ](#access-control-manage-access-intro)
+ [Specifying policy elements: Actions, effects, resources, and principals](#waf-access-control-specify-actions)
+ [Specifying conditions in a policy](#specifying-conditions)

## AWS WAF resources and operations<a name="access-control-resources"></a>

In AWS WAF, the resources are *web ACLs*, *rule groups*, *IP sets*, and *regex pattern sets*\. To allow or deny access to a subset of AWS WAF resources, include the ARN of the resource in the `resource` element of your policy\. The ARNs for AWS WAF resources have the following format:

```
arn:aws:wafv2:region:account:scope/resource/resource/ID
```

The following table lists the format for each resource\. 


****  

| Name in AWS WAF Console | Name in AWS WAF SDK/CLI | ARN Format  | 
| --- | --- | --- | 
| Web ACL | WebACL |  `arn:aws:wafv2:region:account:scope/webacl/name/ID`  | 
| Rule group | RuleGroup |  `arn:aws:wafv2:region:account:scope/rulegroup/name/ID `  | 
| IP set | IPSet | arn:aws:wafv2:region:account:scope/ipset/name/ID | 
| Regex pattern set | RegexPatternSet |  `arn:aws:wafv2:region:account:scope/regexpatternset/name/ID`  | 

To specify an AWS WAF resource ARN, replace the variables in the ARN formats with valid values as follows: 
+ *region*: The AWS Region you're using\. For Amazon CloudFront, set this to `us-east-1`\. For Application Load Balancer or Amazon API Gateway, set this to the region you're interested in\. 
+ *account*: The ID of your AWS account\. 
+ *scope*: The scope of the resource, which can be either `regional`, for use with Application Load Balancer or Amazon API Gateway, or `global`, for use with Amazon CloudFront\. 
+ *name*: The name that you gave the AWS WAF resource, or a wildcard \(`*`\) to indicate all resources of the specified type that are associated with the specified AWS account\. If you use the wildcard for the name, you must also use it for the ID\.
+ *ID*: The ID of the AWS WAF resource, or a wildcard \(`*`\) to indicate all resources of the specified type that are associated with the specified AWS account\. If you use the wildcard for the ID, you must also use it for the name\.

For example, the following ARN specifies all web ACLs with regional scope for the account `111122223333` in Region `us-east-1`:

```
arn:aws:wafv2:us-east-1:111122223333:regional/webacl/*/*
```

For more information, see [Resources](https://docs.aws.amazon.com/IAM/latest/UserGuide/AccessPolicyLanguage_ElementDescriptions.html#Resource) in the *IAM User Guide*\.

AWS WAF provides a set of operations to work with AWS WAF resources\. For a list of available operations, see [Actions](https://docs.aws.amazon.com/waf/latest/APIReference/API_Operations.html)\.

## Understanding resource ownership<a name="access-control-resource-ownership"></a>

A *resource owner* is the AWS account that creates the resource\. That is, the resource owner is the AWS account of the *principal entity* \(the root account, an IAM user, or an IAM role\) that authenticates the request that creates the resource\. The following examples illustrate how this works:
+ If you use the root account credentials of your AWS account to create an AWS WAF resource, your AWS account is the owner of the resource\.
+ If you create an IAM user in your AWS account and grant permissions to create an AWS WAF resource to that user, the user can create an AWS WAF resource\. However, your AWS account, to which the user belongs, owns the AWS WAF resource\.
+ If you create an IAM role in your AWS account with permissions to create an AWS WAF resource, anyone who can assume the role can create an AWS WAF resource\. Your AWS account, to which the role belongs, owns the AWS WAF resource\. 

## Managing access to resources<a name="access-control-manage-access-intro"></a>

A *permissions policy* describes who has access to what\. The following sections explain the available options for creating permissions policies\.

**Note**  
These sections discuss using IAM in the context of AWS WAF\. It doesn't provide detailed information about the IAM service\. For complete IAM documentation, see [What Is IAM?](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) in the *IAM User Guide*\. For information about IAM policy syntax and descriptions, see [AWS IAM Policy Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

Policies that are attached to an IAM identity are known as *identity\-based* policies, and policies that are attached to a resource are known as *resource\-based* policies\. AWS WAF supports only identity\-based policies\.

### Topics<a name="topics2"></a>
+ [Identity\-based policies \(IAM policies\)](#access-control-manage-access-identity-based)
+ [Resource\-based policies](#access-control-manage-access-resource-based)

### Identity\-based policies \(IAM policies\)<a name="access-control-manage-access-identity-based"></a>

You can attach policies to IAM identities\. For example, you can do the following: 
+ **Attach a permissions policy to a user or a group in your account** – An account administrator can use a permissions policy that is associated with a particular user to grant permissions for that user to create an AWS WAF resource\. 
+ **Attach a permissions policy to a role \(grant cross\-account permissions\)** – You can attach an identity\-based permissions policy to an IAM role to grant cross\-account permissions\. For example, the administrator in Account A can create a role to grant cross\-account permissions to another AWS account \(for example, Account B\) or an AWS service as follows:

  1. Account A administrator creates an IAM role and attaches a permissions policy to the role that grants permissions on resources in Account A\.

  1. Account A administrator attaches a trust policy to the role identifying Account B as the principal who can assume the role\. 

  1. Account B administrator can then delegate permissions to assume the role to any users in Account B\. Doing this allows users in Account B to create or access resources in Account A\. The principal in the trust policy also can be an AWS service principal if you want to grant an AWS service permissions to assume the role\.

  For more information about using IAM to delegate permissions, see [Access Management](https://docs.aws.amazon.com/IAM/latest/UserGuide/access.html) in the *IAM User Guide*\. 

The following is an example policy that grants permissions for the `wafv2:ListWebACLs` action on all resources\. In the current implementation, AWS WAF doesn't support identifying specific resources using the resource ARNs \(also referred to as resource\-level permissions\) for some of the API actions, so you must specify a wildcard character \(\*\):

```
{
    "Version": "2019-07-29",
    "Statement": [
        {
            "Sid": "ListWebACLs",
            "Effect": "Allow",
            "Action": [
                "wafv2:ListWebACLs"
            ],
            "Resource": "*"
        }
    ]
}
```

For more information about using identity\-based policies with AWS WAF, see [Using identity\-based policies \(IAM policies\) for AWS WAF](access-control-identity-based.md)\. For more information about users, groups, roles, and permissions, see [Identities \(Users, Groups, and Roles\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id.html) in the *IAM User Guide*\. 

### Resource\-based policies<a name="access-control-manage-access-resource-based"></a>

Other services, such as Amazon S3, also support resource\-based permissions policies\. For example, you can attach a policy to an S3 bucket to manage access permissions to that bucket\. AWS WAF doesn't support resource\-based policies\. 

## Specifying policy elements: Actions, effects, resources, and principals<a name="waf-access-control-specify-actions"></a>

For each AWS WAF resource \(see [AWS WAF resources and operations](#access-control-resources)\), the service defines a set of API operations \(see [AWS WAF API permissions: Actions, resources, and conditions reference](waf-api-permissions-ref.md)\)\. To grant permissions for these API operations, AWS WAF defines a set of actions that you can specify in a policy\. Note that performing an API operation can require permissions for more than one action\. When granting permissions for specific actions, you also identify the resource on which the actions are allowed or denied\.

The following are the most basic policy elements:
+ **Resource** – In a policy, you use an Amazon Resource Name \(ARN\) to identify the resource to which the policy applies\. For more information, see [AWS WAF resources and operations](#access-control-resources)\. 
+ **Action** – You use action keywords to identify resource operations that you want to allow or deny\. For example, the `wafv2:CreateRuleGroup` permission allows the user permissions to perform the AWS WAF `CreateRuleGroup` operation\. 
+ **Effect** – You specify the effect when the user requests the specific action\. This can be either allow or deny\. If you don't explicitly grant access to a resource, access is implicitly denied\. You also can explicitly deny access to a resource, which you might do to make sure that a user cannot access it, even if a different policy grants access\.
+ **Principal** – In identity\-based policies \(IAM policies\), the user that the policy is attached to is the implicit principal\. AWS WAF doesn't support resource\-based policies\.

To learn more about IAM policy syntax and descriptions, see [AWS IAM Policy Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

For a table that shows all the AWS WAF API actions and the resources that they apply to, see [AWS WAF API permissions: Actions, resources, and conditions reference](waf-api-permissions-ref.md)\. 

## Specifying conditions in a policy<a name="specifying-conditions"></a>

When you grant permissions, you can use the IAM policy language to specify the conditions when a policy should take effect\. For example, you might want a policy to be applied only after a specific date\. For more information about specifying conditions in a policy language, see [Condition](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#Condition) in the *IAM User Guide*\.

To express conditions, you use predefined condition keys\. There are no condition keys specific to AWS WAF\. However, there are AWS\-wide condition keys that you can use as appropriate\. For a complete list of AWS\-wide keys, see [Available Keys for Conditions](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\.