# Getting notified of new versions and updates to a managed rule group<a name="waf-using-managed-rule-groups-sns-topic"></a>

You can subscribe to notifications for updates to a managed rule group\. Providers use notifications to announce rule group changes, like upcoming new versions and urgent security updates\. 

**How to subscribe**  
To subscribe to notifications for a rule group, you create an Amazon Simple Notification Service \(Amazon SNS\) subscription for the rule group's Amazon SNS topic ARN in the US East \(N\. Virginia\) Region us\-east\-1\. For information about how to subscribe, see the [Amazon Simple Notification Service Developer Guide](https://docs.aws.amazon.com/sns/latest/dg/)\. 

**Note**  
Create your subscription for the SNS topic only in the us\-east\-1 Region\.

**Where to find the Amazon SNS topic ARN for a managed rule group**
+ **Console** 
  + \(Option\) When you add the managed rule group to your web ACL, choose **Edit** to see the rule group's information, which includes the rule group's Amazon SNS topic ARN\. 
  + \(Option\) After you've added the managed rule group into your web ACL, choose **Edit** on the web ACL, and then select and edit the rule group rule to see the rule group's Amazon SNS topic ARN\. 
+ **API** – `DescribeManagedRuleGroup`
+ **CLI** – `aws wafv2 describe-managed-rule-group --scope=<CLOUDFRONT|REGIONAL> --vendor-name <vendor> --name <managedrule_name>`

**The notification format for AWS Managed Rules**  
The Amazon SNS notifications for AWS Managed Rules rule groups always contain the fields `Subject`, `Message`, and `MessageAttributes`\. Other fields are included according to the type of message and which managed rule group the notification is for\. 

The following shows an example notification listing for the `AWSManagedRulesCommonRuleSet`\.

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

For general information about Amazon SNS notification formats and how to filter the notifications that you receive, see [https://docs\.aws\.amazon\.com/sns/latest/dg/sns\-message\-and\-json\-formats\.html](https://docs.aws.amazon.com/sns/latest/dg/sns-message-and-json-formats.html) and [https://docs\.aws\.amazon\.com/sns/latest/dg/sns\-subscription\-filter\-policies\.html](https://docs.aws.amazon.com/sns/latest/dg/sns-subscription-filter-policies.html) in the Amazon Simple Notification Service Developer Guide\. 