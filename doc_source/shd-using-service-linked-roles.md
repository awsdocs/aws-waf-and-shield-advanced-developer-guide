# Using service\-linked roles for Shield Advanced<a name="shd-using-service-linked-roles"></a>

AWS Shield Advanced uses AWS Identity and Access Management \(IAM\)[ service\-linked roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-linked-role)\. A service\-linked role is a unique type of IAM role that is linked directly to Shield Advanced\. Service\-linked roles are predefined by Shield Advanced and include all the permissions that the service requires to call other AWS services on your behalf\. 

A service\-linked role makes setting up Shield Advanced easier because you don’t have to manually add the necessary permissions\. Shield Advanced defines the permissions of its service\-linked roles, and unless defined otherwise, only Shield Advanced can assume its roles\. The defined permissions include the trust policy and the permissions policy, and that permissions policy cannot be attached to any other IAM entity\.

You can delete a service\-linked role only after first deleting their related resources\. This protects your Shield Advanced resources because you can't inadvertently remove permission to access the resources\.

For information about other services that support service\-linked roles, see [AWS Services That Work with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html) and look for the services that have **Yes **in the **Service\-Linked Role** column\. Choose a **Yes** with a link to view the service\-linked role documentation for that service\.

## Service\-Linked Role Permissions for Shield Advanced<a name="shd-slr-permissions"></a>

Shield Advanced uses the service\-linked role named **AWSServiceRoleForAWSShield**\. This role allows Shield Advanced to access and manage AWS resources in order to automatically respond to application layer DDoS attacks on your behalf\. For more information about this functionality, see [Shield Advanced automatic application layer DDoS mitigation](ddos-automatic-app-layer-response.md)\. 

The AWSServiceRoleForAWSShield service\-linked role trusts the following services to assume the role:
+ `shield.amazonaws.com`

The role permissions policy named AWSShieldServiceRolePolicy allows Shield Advanced to complete the following actions on all AWS resources:
+ `wafv2:GetWebACL`
+ `wafv2:UpdateWebACL`
+ `wafv2:GetWebACLForResource`
+ `wafv2:ListResourcesForWebACL`
+ `cloudfront:ListDistributions`
+ `cloudfront:GetDistribution`

When actions are permitted on all AWS resources, this is indicated in the policy as `"Resource": "*"`\. This only means that the service\-linked role can take each indicated action on all AWS resources *that the action supports*\. For example, the action `wafv2:GetWebACL` is supported only for `wafv2` web ACL resources\. 

Shield Advanced only makes resource\-level API calls for protected resources for which you've enabled the application layer protections feature and for web ACLs that are associated with those protected resources\. 

You must configure permissions to allow an IAM entity \(such as a user, group, or role\) to create, edit, or delete a service\-linked role\. For more information, see [Service\-Linked Role Permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#service-linked-role-permissions) in the *IAM User Guide*\.

## Creating a Service\-Linked Role for Shield Advanced<a name="shd-create-slr"></a>

You don't need to manually create a service\-linked role\. When you enable automatic application layer DDoS mitigation for a resource in the AWS Management Console, the AWS CLI, or the AWS API, Shield Advanced creates the service\-linked role for you\. 

If you delete this service\-linked role, and then need to create it again, you can use the same process to recreate the role in your account\. When you enable automatic application layer DDoS mitigation for a resource, Shield Advanced creates the service\-linked role for you again\. 

## Editing a Service\-Linked Role for Shield Advanced<a name="shd-edit-slr"></a>

Shield Advanced does not allow you to edit the AWSServiceRoleForAWSShield service\-linked role\. After you create a service\-linked role, you cannot change the name of the role because various entities might reference the role\. However, you can edit the description of the role using IAM\. For more information, see [Editing a Service\-Linked Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#edit-service-linked-role) in the *IAM User Guide*\.

## Deleting a Service\-Linked Role for Shield Advanced<a name="shd-delete-slr"></a>

If you no longer need to use a feature or service that requires a service\-linked role, we recommend that you delete that role\. That way you don’t have an unused entity that is not actively monitored or maintained\. However, you must clean up the resources for your service\-linked role before you can manually delete it\.

**Note**  
If Shield Advanced is using the role when you try to delete the resources, then the deletion might fail\. If that happens, wait for a few minutes and try the operation again\.

**To delete the Shield Advanced resources that are used by the AWSServiceRoleForAWSShield**

For all of your resources that have application layer DDoS protections configured, disable automatic application layer DDoS mitigation\. For console instructions, see [Configure application layer DDoS protections](ddos-manage-protected-resources.md#configure-app-layer-protection)\. 

**To manually delete the service\-linked role using IAM**

Use the IAM console, the AWS CLI, or the AWS API to delete the AWSServiceRoleForAWSShield service\-linked role\. For more information, see [Deleting a Service\-Linked Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#delete-service-linked-role) in the *IAM User Guide*\.

## Supported Regions for Shield Advanced Service\-Linked Roles<a name="shd-slr-regions"></a>

Shield Advanced supports using service\-linked roles in all of the Regions where the service is available\. For more information, see [Shield Advanced endpoints and quotas](https://docs.aws.amazon.com/general/latest/gr/shield.html)\.