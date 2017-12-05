# AWS Marketplace Rule Groups<a name="waf-managed-rule-groups"></a>

AWS WAF provides *AWS Marketplace rule groups* to help you protect your resources\. AWS Marketplace rule groups are collections of predefined, ready\-to\-use rules that are written and updated by AWS and AWS partner companies\.

Some AWS Marketplace rule groups are designed to help protect specific types of web applications like WordPress, Joomla, or PHP\. Other AWS Marketplace rule groups offer broad protection against known threats or common web application vulnerabilities, such as those listed in the [OWASP Top 10](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)\.

You can install a single AWS Marketplace rule group from your preferred AWS partner and also add your own customized AWS WAF rules for increased protection\. If you are subject to regulatory compliance like PCI or HIPAA, you might be able to use AWS Marketplace rule groups to satisfy web application firewall requirements\.

 AWS Marketplace rule groups are available with no long\-term contracts, and no minimum commitments\. You are charged a monthly fee \(pro\-rated hourly\) when subscribed to a rule group as well as ongoing request volume\-based fees\. For more information, see [AWS WAF Pricing](https://aws.amazon.com/waf/pricing/) as well as the description for each AWS Marketplace rule group on AWS Marketplace\.

## Automatic Updates<a name="waf-managed-rule-group-updates"></a>

Keeping up to date on the constantly changing threat landscape can be time consuming and expensive\. AWS Marketplace rule groups can save you time when you implement and use AWS WAF\. Another benefit is that AWS and our AWS partners automatically update AWS Marketplace rule groups when new vulnerabilities and threats emerge\.

Many of our partners are notified of new vulnerabilities before public disclosure\. They can update their rule groups and deploy them to you even before a new threat is widely known\. Many also have threat research teams to investigate and analyze the most recent threats in order to write the most relevant rules\.

## Access to the Rules in an AWS Marketplace Rule Group<a name="waf-managed-rule-group-edits"></a>

Each AWS Marketplace rule group provides a comprehensive description of the types of attacks and vulnerabilities that it's designed to protect against\. To protect the intellectual property of the rule group providers, you can't view the individual rules within a rule group\. This restriction also helps to keep malicious users from designing threats that specifically circumvent published rules\.

Because you can’t view individual rules in an AWS Marketplace rule group, you also can't edit any rules in a rule group\. However, you can enable or disable entire rule groups, as well as choose the rule group action to perform\. See [Use AWS Marketplace Rule Groups](#waf-managed-rule-group-using) for more information\. 

## Limits<a name="waf-managed-rule-group-limits"></a>

You can enable only one AWS Marketplace rule group\. This rule group counts towards the 10 rule limit per web ACL\. Therefore you can have one AWS Marketplace rule group and up to nine custom rules in a single web ACL\.

## Pricing<a name="waf-managed-rule-group-pricing"></a>

For AWS Marketplace rule group pricing, see [AWS WAF Pricing](https://aws.amazon.com/waf/pricing/) as well as the description for each AWS Marketplace rule group on AWS Marketplace\.

## Use AWS Marketplace Rule Groups<a name="waf-managed-rule-group-using"></a>

You can subscribe to and unsubscribe from AWS Marketplace rule groups on the AWS WAF console\.

**To subscribe to and use an AWS Marketplace rule group**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/waf/](https://console.aws.amazon.com/waf/)\. 

1. In the navigation pane, choose **Marketplace**\.

1. In the **Available marketplace products** section, choose the name of a rule group to view the details and pricing information\.

1. If you want to subscribe to the rule group, choose **Continue**\.
**Note**  
If you don't want to subscribe to this rule group, simply close this page in your browser\.

1. Choose **Set up your account**\.

1. Add the rule group to a web ACL, just as you would add an individual rule\. For more information, see [Creating a Web ACL](web-acl-creating.md) or [Editing a Web ACL](web-acl-editing.md)\.
**Note**  
When adding a rule group to a web ACL, the action you set for the rule group \(either **No override** or **Override to count**\) is called the rule group override action\. For more information, see [Rule Group Override](#waf-managed-rule-group-override)\.

**To unsubscribe from an AWS Marketplace rule group**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/waf/](https://console.aws.amazon.com/waf/)\. 

1. Remove the rule group from all web ACLs\. For more information, see [Editing a Web ACL](web-acl-editing.md)\.

1. In the navigation pane, choose **Marketplace**\.

1. Choose **Manage your subscriptions**\.

1. Choose **Cancel subscription** next to the name of the rule group that you want to unsubscribe from\.

1. Choose **Yes, cancel subscription**\.

## Rule Group Override<a name="waf-managed-rule-group-override"></a>

AWS Marketplace rule groups have two possible actions: **No override** and **Override to count**\. If you want to test the rule group, set the action to **Override to count**\. This rule group action will then override any *block* action specified by individual rules contained within the group\. That is, if the rule group's action is set to **Override to count**, instead of potentially blocking matching requests based on the action of individual rules within the group, those requests will be counted\. Conversely, if you set the rule group's action to **No override**, actions of the individual rules within the group will be used\.

## Troubleshooting AWS Marketplace Rule Groups<a name="waf-managed-rule-group-troubleshooting"></a>

If you find that an AWS Marketplace rule group is blocking legitimate traffic, perform the following steps\.

**To troubleshoot an AWS Marketplace rule group**

1. Change the action for the AWS Marketplace rule group from **No override** to **Override to count**\. This allows the web request to pass through, regardless of the individual rule actions within the rule group\. This also provides you with Amazon CloudWatch metrics for the rule group\.

1. After setting the AWS Marketplace rule group action to **Override to count**, contact the rule group provider‘s customer support team to further troubleshoot the issue\. For contact information, see rule group listing on the product listing pages on AWS Marketplace\.

### Contacting Customer Support<a name="waf-managed-rule-group-troubleshooting-support"></a>

For problems with AWS WAF or a rule group that is managed by AWS, contact AWS Support\. For problems with a rule group that is managed by an AWS partner, contact that partner's customer support team\. To find partner contact information, see the partner’s listing on AWS Marketplace\.

## Creating and Selling AWS Marketplace Rule Groups<a name="waf-managed-rule-group-creating"></a>

If you want to sell AWS Marketplace rule groups on AWS Marketplace, see [How to Sell Your Software on AWS Marketplace](https://aws.amazon.com/marketplace/management/tour/)\.