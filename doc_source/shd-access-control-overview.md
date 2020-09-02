# Overview of managing access permissions to your AWS Shield resources<a name="shd-access-control-overview"></a>

Every AWS resource is owned by an AWS account, and permissions to create or access a resource are governed by permissions policies\. An account administrator can attach permissions policies to IAM identities \(that is, users, groups, and roles\)\. Some services also support attaching permissions policies to resources\.

**Note**  
An *account administrator* \(or administrator user\) is a user with administrator privileges\. For more information, see [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) in the *IAM User Guide*\.

When granting permissions, you decide who is getting the permissions, the resources they get permissions for, and the specific operations that you want to allow on those resources\.

## Topics<a name="shd-topics1"></a>
+ [AWS Shield resources and operations](#shd-access-control-resources)
+ [Understanding resource ownership](#shd-access-control-resource-ownership)
+  [Managing access to resources ](#shd-access-control-manage-access-intro)
+ [Specifying policy elements: Actions, effects, resources, and principals](#shd-access-control-specify-actions)
+ [Specifying conditions in a policy](#shd-specifying-conditions)

## AWS Shield resources and operations<a name="shd-access-control-resources"></a>

In AWS Shield, the resources are *protections* and *attacks*\. These resources have unique Amazon Resource Names \(ARNs\) associated with them, as shown in the following table\. 


****  

| Name in AWS Shield Console | Name in AWS Shield SDK/CLI | ARN Format  | 
| --- | --- | --- | 
| Event or attack | AttackDetail |  `arn:aws:shield::account:attack/ID`  | 
| Protection | Protection |  `arn:aws:shield::account:protection/ID`  | 

To allow or deny access to a subset of Shield resources, include the ARN of the resource in the `resource` element of your policy\. The ARNs for Shield have the following format:

```
arn:aws:shield::account:resource/ID
```

Replace the *account*, *resource*, and *ID* variables with valid values\. Valid values can be the following:
+ *account*: The ID of your AWS account\. You must specify a value\.
+ *resource*: The type of Shield resource\. 
+ *ID*: The ID of the Shield resource, or a wildcard \(`*`\) to indicate all resources of the specified type that are associated with the specified AWS account\.

For example, the following ARN specifies all protections for the account `111122223333`:

```
arn:aws:shield::111122223333:protection/*
```

For more information, see [Resources](https://docs.aws.amazon.com/IAM/latest/UserGuide/AccessPolicyLanguage_ElementDescriptions.html#Resource) in the *IAM User Guide*\.

AWS Shield provides a set of operations to work with Shield resources\. For a list of available operations, see [Actions](https://docs.aws.amazon.com/waf/latest/DDOSAPIReference/API_Operations.html)\.

## Understanding resource ownership<a name="shd-access-control-resource-ownership"></a>

A *resource owner* is the AWS account that creates the resource\. That is, the resource owner is the AWS account of the *principal entity* \(the root account, an IAM user, or an IAM role\) that authenticates the request that creates the resource\. The following examples illustrate how this works:
+ If you use the root account credentials of your AWS account to create a Shield resource, your AWS account is the owner of the resource\.
+ If you create an IAM user in your AWS account and grant permissions to create a Shield resource to that user, the user can create a Shield resource\. However, your AWS account, to which the user belongs, owns the Shield resource\.
+ If you create an IAM role in your AWS account with permissions to create a Shield resource, anyone who can assume the role can create a Shield resource\. Your AWS account, to which the role belongs, owns the Shield resource\. 
+ With AWS Shield, to create a protection or describe an attack associated with a specific resource, a user must have an access to the resource itself in addition to having access to the Shield resource\. For example to create a protection for an Amazon CloudFront distribution, the user needs read access for the distribution to protect\. To describe an attack against a CloudFront distribution, the user needs read access to the distribution\.

## Managing access to resources<a name="shd-access-control-manage-access-intro"></a>

A *permissions policy* describes who has access to what\. The following sections explain the available options for creating permissions policies\.

**Note**  
These sections discuss using IAM in the context of AWS Shield\. It doesn't provide detailed information about the IAM service\. For complete IAM documentation, see [What Is IAM?](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) in the *IAM User Guide*\. For information about IAM policy syntax and descriptions, see [AWS IAM Policy Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

Policies that are attached to an IAM identity are known as *identity\-based* policies, and policies that are attached to a resource are known as *resource\-based* policies\. AWS Shield supports only identity\-based policies\.

### Topics<a name="shd-topics2"></a>
+ [Identity\-based policies \(IAM policies\)](#shd-access-control-manage-access-identity-based)
+ [Resource\-based policies](#shd-access-control-manage-access-resource-based)

### Identity\-based policies \(IAM policies\)<a name="shd-access-control-manage-access-identity-based"></a>

You can attach policies to IAM identities\. For example, you can do the following: 
+ **Attach a permissions policy to a user or a group in your account** – An account administrator can use a permissions policy that is associated with a particular user to grant permissions for that user to create an Shield resource\. 
+ **Attach a permissions policy to a role \(grant cross\-account permissions\)** – You can attach an identity\-based permissions policy to an IAM role to grant cross\-account permissions\. For example, the administrator in Account A can create a role to grant cross\-account permissions to another AWS account \(for example, Account B\) or an AWS service as follows:

  1. Account A administrator creates an IAM role and attaches a permissions policy to the role that grants permissions on resources in Account A\.

  1. Account A administrator attaches a trust policy to the role identifying Account B as the principal who can assume the role\. 

  1. Account B administrator can then delegate permissions to assume the role to any users in Account B\. Doing this allows users in Account B to create or access resources in Account A\. The principal in the trust policy also can be an AWS service principal if you want to grant an AWS service permissions to assume the role\.

  For more information about using IAM to delegate permissions, see [Access Management](https://docs.aws.amazon.com/IAM/latest/UserGuide/access.html) in the *IAM User Guide*\. 

  AWS Shield allows cross\-account resource access, but it doesn't allow you to create cross\-account resource protections\. You can only create protections for resources from within the account that owns those resources\. 

The following is an example policy that grants permissions for the `shield:ListProtections` action on all resources\. Shield doesn't support identifying specific resources using the resource ARNs \(also referred to as resource\-level permissions\) for some of the API actions, so you must specify a wildcard character \(\*\):

```
{
    "Version": "2016-06-02",
    "Statement": [
        {
            "Sid": "ListProtections",
            "Effect": "Allow",
            "Action": [
                "shield:ListProtections"
            ],
            "Resource": "*"
        }
    ]
}
```

For more information about using identity\-based policies with Shield, see [Using identity\-based policies \(IAM policies\) for AWS Shield](shd-access-control-identity-based.md)\. For more information about users, groups, roles, and permissions, see [Identities \(Users, Groups, and Roles\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id.html) in the *IAM User Guide*\. 

### Resource\-based policies<a name="shd-access-control-manage-access-resource-based"></a>

Other services, such as Amazon S3, also support resource\-based permissions policies\. For example, you can attach a policy to an S3 bucket to manage access permissions to that bucket\. AWS Shield doesn't support resource\-based policies\. 

## Specifying policy elements: Actions, effects, resources, and principals<a name="shd-access-control-specify-actions"></a>

For each AWS Shield resource \(see [AWS Shield resources and operations](#shd-access-control-resources)\), the service defines a set of API operations \(see [Shield required permissions for API actions](shd-api-permissions-ref.md)\)\. To grant permissions for these API operations, Shield defines a set of actions that you can specify in a policy\. Note that performing an API operation can require permissions for more than one action\. When granting permissions for specific actions, you also identify the resource on which the actions are allowed or denied\.

The following are the most basic policy elements:
+ **Resource** – In a policy, you use an Amazon Resource Name \(ARN\) to identify the resource to which the policy applies\. For more information, see [AWS Shield resources and operations](#shd-access-control-resources)\. 
+ **Action** – You use action keywords to identify resource operations that you want to allow or deny\. For example, the `shield:CreateRuleGroup` permission allows the user permissions to perform the AWS Shield `CreateRuleGroup` operation\. 
+ **Effect** – You specify the effect when the user requests the specific action\. This can be either allow or deny\. If you don't explicitly grant access to a resource, access is implicitly denied\. You also can explicitly deny access to a resource, which you might do to make sure that a user cannot access it, even if a different policy grants access\.
+ **Principal** – In identity\-based policies \(IAM policies\), the user that the policy is attached to is the implicit principal\. AWS Shield doesn't support resource\-based policies\.

To learn more about IAM policy syntax and descriptions, see [AWS IAM Policy Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

For a table that shows all the AWS Shield API actions and the resources that they apply to, see [Shield required permissions for API actions](shd-api-permissions-ref.md)\. 

## Specifying conditions in a policy<a name="shd-specifying-conditions"></a>

When you grant permissions, you can use the IAM policy language to specify the conditions when a policy should take effect\. For example, you might want a policy to be applied only after a specific date\. For more information about specifying conditions in a policy language, see [Condition](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#Condition) in the *IAM User Guide*\.

To express conditions, you use predefined condition keys\. There are no condition keys specific to Shield\. However, there are AWS\-wide condition keys that you can use as appropriate\. For a complete list of AWS\-wide keys, see [Available Keys for Conditions](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\.