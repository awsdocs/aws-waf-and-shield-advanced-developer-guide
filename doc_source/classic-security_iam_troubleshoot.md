# Troubleshooting AWS WAF Classic identity and access<a name="classic-security_iam_troubleshoot"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

Use the following information to help you diagnose and fix common issues that you might encounter when working with AWS WAF Classic and IAM\.

**Topics**
+ [I am not authorized to perform an action in AWS WAF Classic](#classic-security_iam_troubleshoot-no-permissions)
+ [I am not authorized to perform iam:PassRole](#classic-security_iam_troubleshoot-passrole)
+ [I want to allow people outside of my AWS account to access my AWS WAF Classic resources](#classic-security_iam_troubleshoot-cross-account-access)

## I am not authorized to perform an action in AWS WAF Classic<a name="classic-security_iam_troubleshoot-no-permissions"></a>

If you receive an error that you're not authorized to perform an action, your policies must be updated to allow you to perform the action\.

The following example error occurs when the `mateojackson` IAM user tries to use the console to view details about a fictional `my-example-widget` resource but doesn't have the fictional `waf:GetWidget` permissions\.

```
User: arn:aws:iam::123456789012:user/mateojackson is not authorized to perform: waf:GetWidget on resource: my-example-widget
```

In this case, the policy for the `mateojackson` user must be updated to allow access to the `my-example-widget` resource by using the `waf:GetWidget` action\.

If you need help, contact your AWS administrator\. Your administrator is the person who provided you with your sign\-in credentials\.

## I am not authorized to perform iam:PassRole<a name="classic-security_iam_troubleshoot-passrole"></a>

If you receive an error that you're not authorized to perform the `iam:PassRole` action, your policies must be updated to allow you to pass a role to AWS WAF Classic\.

Some AWS services allow you to pass an existing role to that service instead of creating a new service role or service\-linked role\. To do this, you must have permissions to pass the role to the service\.

The following example error occurs when an IAM user named `marymajor` tries to use the console to perform an action in AWS WAF Classic\. However, the action requires the service to have permissions that are granted by a service role\. Mary does not have permissions to pass the role to the service\.

```
User: arn:aws:iam::123456789012:user/marymajor is not authorized to perform: iam:PassRole
```

In this case, Mary's policies must be updated to allow her to perform the `iam:PassRole` action\.

If you need help, contact your AWS administrator\. Your administrator is the person who provided you with your sign\-in credentials\.

## I want to allow people outside of my AWS account to access my AWS WAF Classic resources<a name="classic-security_iam_troubleshoot-cross-account-access"></a>

You can create a role that users in other accounts or people outside of your organization can use to access your resources\. You can specify who is trusted to assume the role\. For services that support resource\-based policies or access control lists \(ACLs\), you can use those policies to grant people access to your resources\.

To learn more, consult the following:
+ To learn whether AWS WAF Classic supports these features, see [How AWS WAF Classic works with IAM](classic-security_iam_service-with-iam.md)\.
+ To learn how to provide access to your resources across AWS accounts that you own, see [Providing access to an IAM user in another AWS account that you own](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios_aws-accounts.html) in the *IAM User Guide*\.
+ To learn how to provide access to your resources to third\-party AWS accounts, see [Providing access to AWS accounts owned by third parties](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios_third-party.html) in the *IAM User Guide*\.
+ To learn how to provide access through identity federation, see [Providing access to externally authenticated users \(identity federation\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios_federated-users.html) in the *IAM User Guide*\.
+ To learn the difference between using roles and resource\-based policies for cross\-account access, see [How IAM roles differ from resource\-based policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_compare-resource-policies.html) in the *IAM User Guide*\.