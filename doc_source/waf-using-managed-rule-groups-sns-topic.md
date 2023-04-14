# Getting notified of new versions and updates to a managed rule group<a name="waf-using-managed-rule-groups-sns-topic"></a>

A managed rule group provider uses SNS notifications to announce rule group changes, like upcoming new versions and urgent security updates\. 

**How to subscribe to SNS notifications**  
To subscribe to notifications for a rule group, you create an Amazon SNS subscription for the rule group's Amazon SNS topic ARN in the US East \(N\. Virginia\) Region us\-east\-1\. 

For information about how to subscribe, see the [Amazon Simple Notification Service Developer Guide](https://docs.aws.amazon.com/sns/latest/dg/)\. 

**Note**  
Create your subscription for the SNS topic only in the us\-east\-1 Region\.

**Where to find the Amazon SNS topic ARN for a managed rule group**

AWS Managed Rules rule groups use a single SNS topic ARN, so you can retrieve the topic ARN from one of the rule groups and subscribe to it to get notifications for all of the AWS Managed Rules rule groups that provide SNS notifications\. 
+ **Console** 
  + \(Option\) When you add the managed rule group to your web ACL, choose **Edit** to see the rule group's information, which includes the rule group's Amazon SNS topic ARN\. 
  + \(Option\) After you've added the managed rule group into your web ACL, choose **Edit** on the web ACL, and then select and edit the rule group rule to see the rule group's Amazon SNS topic ARN\. 
+ **API** – `DescribeManagedRuleGroup`
+ **CLI** – `aws wafv2 describe-managed-rule-group --scope=<CLOUDFRONT|REGIONAL> --vendor-name <vendor> --name <managedrule_name>`

**Versioning and SNS notifications for AWS Managed Rules rule groups**  
The AWS Managed Rules rule groups all provide versioning and SNS update notifications except for the rule groups for IP reputation, Bot Control, and account takeover prevention\. 

The AWS Managed Rules rule groups that provide notifications all use the same SNS topic Amazon Resource Name \(ARN\)\.

For deployments that affect your protections, such as changes to the default version, AWS provides SNS notifications to inform you of planned deployments and to let you know when a deployment is starting\. For deployments that don't affect your protections, such as release candidate and static version deployments, AWS might notify you after the deployment has started or even after it's completed\. At the completion of the deployment of a new static version, AWS updates this guide, in the changelog at [AWS Managed Rules changelog](aws-managed-rule-groups-changelog.md) and in the document history page at [Document history](doc-history.md)\. For more information about the notifications provided for each type of deployment, see [Deployments for versioned AWS Managed Rules rule groups ](waf-managed-rule-groups-deployments.md)\.

To receive all updates that AWS provides for the AWS Managed Rules rule groups, subscribe to the RSS feed from any HTML page of this guide, and subscribe to the SNS topic for the AWS Managed Rules rule groups\. 

The fields in the Amazon SNS notifications always include the Subject, Message, and MessageAttributes\. Additional fields depend on the type of message and which managed rule group the notification is for\. The following shows an example notification listing for `AWSManagedRulesCommonRuleSet`\.

```
{
    "Type": "Notification",
    "MessageId": "4286b830-a463-5e61-bd15-e1ae72303868",
    "TopicArn": "arn:aws:sns:us-west-2:123456789012:MyTopic",
    "Subject": "New version available for rule group AWSManagedRulesCommonRuleSet",
    "Message": "Welcome to AWSManagedRulesCommonRuleSet version 1.5! We've updated the regex specification in this version to improve protection coverage, adding protections against insecure deserialization. For details about this change, see http://updatedPublicDocs.html. Look for more exciting updates in the future! ",
    "Timestamp": "2021-08-24T11:12:19.810Z",
    "SignatureVersion": "1",
    "Signature": "EXAMPLEHXgJm...",
    "SigningCertURL": "https://sns.us-west-2.amazonaws.com/SimpleNotificationService-f3ecfb7224c7233fe7bb5f59f96de52f.pem",
    "SubscribeURL": "https://sns.us-west-2.amazonaws.com/?Action=ConfirmSubscription&TopicArn=arn:aws:sns:us-west-2:123456789012:MyTopic&Token=2336412f37...",
    "MessageAttributes": {
        "major_version": {
            "Type": "String",
            "Value": "v1"
        },
        "managed_rule_group": {
            "Type": "String",
            "Value": "AWSManagedRulesCommonRuleSet"
        }
    }
}
```

For general information about Amazon SNS notification formats and how to filter the notifications that you receive, see [Parsing message formats](https://docs.aws.amazon.com/sns/latest/dg/sns-message-and-json-formats.html) and [Amazon SNS subscription filter policies](https://docs.aws.amazon.com/sns/latest/dg/sns-subscription-filter-policies.html) in the Amazon Simple Notification Service Developer Guide\. 