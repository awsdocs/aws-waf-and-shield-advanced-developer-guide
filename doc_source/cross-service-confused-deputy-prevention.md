# Cross\-service confused deputy prevention<a name="cross-service-confused-deputy-prevention"></a>

The confused deputy problem is a security issue where an entity that doesn't have permission to perform an action can coerce a more\-privileged entity to perform the action\. In AWS, cross\-service impersonation can result in the confused deputy problem\. Cross\-service impersonation can occur when one service \(the *calling service*\) calls another service \(the *called service*\)\. The calling service can be manipulated to use its permissions to act on another customer's resources in a way it should not otherwise have permission to access\. To prevent this, AWS provides tools that help you protect your data for all services with service principals that have been given access to resources in your account\. 

We recommend using the [https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourcearn](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourcearn) and [https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourceaccount](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourceaccount) global condition context keys in resource policies to limit the permissions that AWS Firewall Manager gives another service to the resource\. Use `aws:SourceArn` if you want only one resource to be associated with the cross\-service access\. Use `aws:SourceAccount` if you want to allow any resource in that account to be associated with the cross\-service use\.

The most effective way to protect against the confused deputy problem is to use the `aws:SourceArn` global condition context key with the full ARN of the resource\. If you don't know the full ARN of the resource or if you are specifying multiple resources, use the `aws:SourceArn` global context condition key with wildcard characters \(`*`\) for the unknown portions of the ARN\. For example, `arn:aws:fms:*:account-id:*`\. 

If the `aws:SourceArn` value does not contain the account ID, such as an Amazon S3 bucket ARN, you must use both global condition context keys to limit permissions\. 

The value of `aws:SourceArn` must be the AWS Firewall Manager administrator's AWS account\.

The following examples show how you can use the `aws:SourceArn` global condition context key in Firewall Manager to prevent the confused deputy problem\.

The following example shows how to prevent the confused deputy problem by using the `aws:SourceArn` global condition context key in the Firewall Manager role trust policy\. Replace *Region* and *account\-id* with your own information\.

```
{
  "Version": "2012-10-17",
  "Statement": {
    "Sid": "ConfusedDeputyPreventionExamplePolicy",
    "Effect": "Allow",
    "Principal": {
      "Service": "servicename.amazonaws.com"
    },
    "Action": "sts:AssumeRole",
    "Condition": {
      "ArnLike": {
        "aws:SourceArn": [
          "arn:aws:fms:Region:account-id:${*}",
          "arn:aws:fms:Region:account-id:policy/*"]
      },
      "StringEquals": {
        "aws:SourceAccount": "account-id"
      }
    }
  }
}
```