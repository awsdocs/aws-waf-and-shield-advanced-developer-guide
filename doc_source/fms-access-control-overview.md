# Overview of managing access permissions to your AWS Firewall Manager resources<a name="fms-access-control-overview"></a>

Every AWS resource is owned by an AWS account, and permissions to create or access a resource are governed by permissions policies\. An account administrator can attach permissions policies to IAM identities \(that is, users, groups, and roles\)\. Some services also support attaching permissions policies to resources\.

**Note**  
An *account administrator* \(or administrator user\) is a user with administrator privileges\. For more information, see [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html) in the *IAM User Guide*\.

When granting permissions, you decide who is getting the permissions, the resources they get permissions for, and the specific operations that you want to allow on those resources\.

## Topics<a name="fms-topics1"></a>
+ [AWS Firewall Manager resources and operations](#fms-access-control-resources)
+ [Understanding resource ownership](#fms-access-control-resource-ownership)
+  [Managing access to resources ](#fms-access-control-manage-access-intro)
+ [Specifying policy elements: Actions, effects, resources, and principals](#fms-access-control-specify-actions)
+ [Specifying conditions in a policy](#fms-specifying-conditions)

## AWS Firewall Manager resources and operations<a name="fms-access-control-resources"></a>

In AWS Firewall Manager, the resources are *policy*, *applications list*, and *protocols list*\. The Amazon Resource Name \(ARN\) for Firewall Manager resources has the following format: 

```
arn:aws:fms:region:account:resource/ID
```

The following table lists the format for each resource\. 


****  

| Name in AWS Firewall Manager Console | Name in AWS Firewall Manager SDK/CLI | ARN Format  | 
| --- | --- | --- | 
| Policy | Policy |  `arn:aws:fms:region:account:policy/ID`  | 
| Applications list | AppsList |  `arn:aws:fms:region:account:applications-list/ID`  | 
| Protocols list | ProtocolsList |  `arn:aws:fms:region:account:protocols-list/ID`  | 

To allow or deny access to a subset of Firewall Manager resources, include the ARNs of the resources in the `resource` element of your policy\. Replace the *account*, *resource*, and *ID* variables with valid values\. Valid values can be the following:
+ *account*: The ID of your AWS account\. You must specify a value\.
+ *resource*: The type of Firewall Manager resource\. 
+ *ID*: The ID of the Firewall Manager resource, or a wildcard \(`*`\) to indicate all resources of the specified type that are associated with the specified AWS account\.

For example, the following ARN specifies all policies for the account `111122223333` in Region `us-east-1`:

```
arn:aws:fms:us-east-1:111122223333:policy/*
```

For more information, see [Resources](https://docs.aws.amazon.com/IAM/latest/UserGuide/AccessPolicyLanguage_ElementDescriptions.html#Resource) in the *IAM User Guide*\.

AWS Firewall Manager provides a set of operations to work with Firewall Manager resources\. For a list of available operations, see [Actions](https://docs.aws.amazon.com/fms/2018-01-01/APIReference/API_Operations.html)\.

## Understanding resource ownership<a name="fms-access-control-resource-ownership"></a>

A *resource owner* is the AWS account that creates the resource\. That is, the resource owner is the AWS account of the *principal entity* \(the root account, an IAM user, or an IAM role\) that authenticates the request that creates the resource\. The following examples illustrate how this works:
+ If you use the root account credentials of your AWS account to create a Firewall Manager resource, your AWS account is the owner of the resource\.
+ If you create an IAM user in your AWS account and grant permissions to create a Firewall Manager resource to that user, the user can create a Firewall Manager resource\. However, your AWS account, to which the user belongs, owns the Firewall Manager resource\.
+ If you create an IAM role in your AWS account with permissions to create a Firewall Manager resource, anyone who can assume the role can create a Firewall Manager resource\. Your AWS account, to which the role belongs, owns the Firewall Manager resource\. 

## Managing access to resources<a name="fms-access-control-manage-access-intro"></a>

A *permissions policy* describes who has access to what\. The following sections explain the available options for creating permissions policies\.

**Note**  
These sections discuss using IAM in the context of AWS Firewall Manager\. It doesn't provide detailed information about the IAM service\. For complete IAM documentation, see [What Is IAM?](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html) in the *IAM User Guide*\. For information about IAM policy syntax and descriptions, see [AWS IAM Policy Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

Policies that are attached to an IAM identity are known as *identity\-based* policies, and policies that are attached to a resource are known as *resource\-based* policies\. AWS Firewall Manager supports only identity\-based policies\.

### Topics<a name="fms-topics2"></a>
+ [Identity\-based policies \(IAM policies\)](#fms-access-control-manage-access-identity-based)
+ [Resource\-based policies](#fms-access-control-manage-access-resource-based)

### Identity\-based policies \(IAM policies\)<a name="fms-access-control-manage-access-identity-based"></a>

You can attach policies to IAM identities\. For example, you can do the following: 
+ **Attach a permissions policy to a user or a group in your account** – An account administrator can use a permissions policy that is associated with a particular user to grant permissions for that user to create a Firewall Manager resource\. 
+ **Attach a permissions policy to a role \(grant cross\-account permissions\)** – You can attach an identity\-based permissions policy to an IAM role to grant cross\-account permissions\. For example, the administrator in Account A can create a role to grant cross\-account permissions to another AWS account \(for example, Account B\) or an AWS service as follows:

  1. Account A administrator creates an IAM role and attaches a permissions policy to the role that grants permissions on resources in Account A\.

  1. Account A administrator attaches a trust policy to the role identifying Account B as the principal who can assume the role\. 

  1. Account B administrator can then delegate permissions to assume the role to any users in Account B\. Doing this allows users in Account B to create or access resources in Account A\. The principal in the trust policy also can be an AWS service principal if you want to grant an AWS service permissions to assume the role\.

  For more information about using IAM to delegate permissions, see [Access Management](https://docs.aws.amazon.com/IAM/latest/UserGuide/access.html) in the *IAM User Guide*\. 

The following is an example policy that grants permissions for the `fms:GetPolicy` action on all policies in two specific regions\. 

```
{
"Version": "2012-10-17",
"Statement": [
   {
       "Sid": "VisualEditor0",
       "Effect": "Deny",
       "Action": "fms:GetPolicy",
       "Resource": [
           "arn:aws:fms:us-east-1:*:policy/*",
           "arn:aws:fms:us-west-2:*:policy/*"
       ],
       "Condition": {
           "StringEquals": {
               "aws:ResourceTag/stage": "prod"
           }
       }
   }
]
}
```

For more information about using identity\-based policies with Firewall Manager, see [Using identity\-based policies \(IAM policies\) for AWS Firewall Manager](fms-access-control-identity-based.md)\. For more information about users, groups, roles, and permissions, see [Identities \(Users, Groups, and Roles\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id.html) in the *IAM User Guide*\. 

### Resource\-based policies<a name="fms-access-control-manage-access-resource-based"></a>

Other services, such as Amazon S3, also support resource\-based permissions policies\. For example, you can attach a policy to an S3 bucket to manage access permissions to that bucket\. AWS Firewall Manager doesn't support resource\-based policies\. 

## Specifying policy elements: Actions, effects, resources, and principals<a name="fms-access-control-specify-actions"></a>

For each AWS Firewall Manager resource \(see [AWS Firewall Manager resources and operations](#fms-access-control-resources)\), the service defines a set of API operations \(see [Firewall Manager required permissions for API actions](fms-api-permissions-ref.md)\)\. To grant permissions for these API operations, Firewall Manager defines a set of actions that you can specify in a policy\. Note that performing an API operation can require permissions for more than one action\. When granting permissions for specific actions, you also identify the resource on which the actions are allowed or denied\.

The following are the most basic policy elements:
+ **Resource** – In a policy, you use an Amazon Resource Name \(ARN\) to identify the resource to which the policy applies\. For more information, see [AWS Firewall Manager resources and operations](#fms-access-control-resources)\. 
+ **Action** – You use action keywords to identify resource operations that you want to allow or deny\. For example, the `fms:CreatePolicy` permission, coupled with the `wafv2:ListRuleGroups` permission, allows the user permissions to perform the AWS Firewall Manager `CreatePolicy` operation\. 
+ **Effect** – You specify the effect when the user requests the specific action\. This can be either allow or deny\. If you don't explicitly grant access to a resource, access is implicitly denied\. You also can explicitly deny access to a resource, which you might do to make sure that a user cannot access it, even if a different policy grants access\.
+ **Principal** – In identity\-based policies \(IAM policies\), the user that the policy is attached to is the implicit principal\. AWS Firewall Manager doesn't support resource\-based policies\.

To learn more about IAM policy syntax and descriptions, see [AWS IAM Policy Reference](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies.html) in the *IAM User Guide*\.

For a table that shows all the AWS Firewall Manager API actions and the resources that they apply to, see [Firewall Manager required permissions for API actions](fms-api-permissions-ref.md)\. 

## Specifying conditions in a policy<a name="fms-specifying-conditions"></a>

When you grant permissions, you can use the IAM policy language to specify the conditions when a policy should take effect\. For example, you might want a policy to be applied only after a specific date\. For more information about specifying conditions in a policy language, see [Condition](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#Condition) in the *IAM User Guide*\.

To express conditions, you use predefined condition keys\. There are no condition keys specific to Firewall Manager\. However, there are AWS\-wide condition keys that you can use as appropriate\. For a complete list of AWS\-wide keys, see [Available Keys for Conditions](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\.