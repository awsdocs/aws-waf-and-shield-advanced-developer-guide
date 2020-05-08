# AWS marketplace rule groups<a name="classic-waf-managed-rule-groups"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

AWS WAF Classic provides *AWS Marketplace rule groups* to help you protect your resources\. AWS Marketplace rule groups are collections of predefined, ready\-to\-use rules that are written and updated by AWS and AWS partner companies\.

Some AWS Marketplace rule groups are designed to help protect specific types of web applications like WordPress, Joomla, or PHP\. Other AWS Marketplace rule groups offer broad protection against known threats or common web application vulnerabilities, such as those listed in the [OWASP Top 10](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)\.

You can install a single AWS Marketplace rule group from your preferred AWS partner, and you can also add your own customized AWS WAF Classic rules for increased protection\. If you are subject to regulatory compliance like PCI or HIPAA, you might be able to use AWS Marketplace rule groups to satisfy web application firewall requirements\.

 AWS Marketplace rule groups are available with no long\-term contracts, and no minimum commitments\. When you subscribe to a rule group, you are charged a monthly fee \(prorated hourly\) and ongoing request fees based on volume\. For more information, see [AWS WAF Classic Pricing](https://aws.amazon.com/waf/pricing/) and the description for each AWS Marketplace rule group on AWS Marketplace\.

## Automatic updates<a name="classic-waf-managed-rule-group-updates"></a>

Keeping up to date on the constantly changing threat landscape can be time consuming and expensive\. AWS Marketplace rule groups can save you time when you implement and use AWS WAF Classic\. Another benefit is that AWS and our AWS partners automatically update AWS Marketplace rule groups when new vulnerabilities and threats emerge\.

Many of our partners are notified of new vulnerabilities before public disclosure\. They can update their rule groups and deploy them to you even before a new threat is widely known\. Many also have threat research teams to investigate and analyze the most recent threats in order to write the most relevant rules\.

## Access to the rules in an AWS marketplace rule group<a name="classic-waf-managed-rule-group-edits"></a>

Each AWS Marketplace rule group provides a comprehensive description of the types of attacks and vulnerabilities that it's designed to protect against\. To protect the intellectual property of the rule group providers, you can't view the individual rules within a rule group\. This restriction also helps to keep malicious users from designing threats that specifically circumvent published rules\.

Because you can’t view individual rules in an AWS Marketplace rule group, you also can't edit any rules in an AWS Marketplace rule group\. However, you can exclude specific rules from a rule group\. This is called a "rule group exception\." Excluding rules does not remove those rules\. Rather, it changes the action for the rules to `COUNT`\. Therefore, requests that match an excluded rule are counted but not blocked\. You will receive COUNT metrics for each excluded rule\.

Excluding rules can be helpful when troubleshooting rule groups that are blocking traffic unexpectedly \(false positives\)\. One troubleshooting technique is to identify the specific rule within the rule group that is blocking the desired traffic and then disable \(exclude\) that particular rule\.

In addition to excluding specific rules, you can refine your protection by enabling or disabling entire rule groups, as well as choosing the rule group action to perform\. For more information, see [Using AWS marketplace rule groups](#classic-waf-managed-rule-group-using)\. 

## Quotas<a name="classic-waf-managed-rule-group-limits"></a>

You can enable only one AWS Marketplace rule group\. You can also enable one custom rule group that you create using AWS Firewall Manager\. These rule groups count towards the 10 rule maximum quota per web ACL\. Therefore, you can have one AWS Marketplace rule group, one custom rule group, and up to eight custom rules in a single web ACL\.

## Pricing<a name="classic-waf-managed-rule-group-pricing"></a>

For AWS Marketplace rule group pricing, see [AWS WAF Classic Pricing](https://aws.amazon.com/waf/pricing/) and the description for each AWS Marketplace rule group on AWS Marketplace\.

## Using AWS marketplace rule groups<a name="classic-waf-managed-rule-group-using"></a>

You can subscribe to and unsubscribe from AWS Marketplace rule groups on the AWS WAF Classic console\. You can also exclude specific rules from a rule group\.<a name="classic-waf-managed-rule-group-using-procedure"></a>

**To subscribe to and use an AWS marketplace rule group**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Marketplace**\.

1. In the **Available marketplace products** section, choose the name of a rule group to view the details and pricing information\.

1. If you want to subscribe to the rule group, choose **Continue**\.
**Note**  
If you don't want to subscribe to this rule group, simply close this page in your browser\.

1. Choose **Set up your account**\.

1. Add the rule group to a web ACL, just as you would add an individual rule\. For more information, see [Creating a Web ACL](classic-web-acl-creating.md) or [Editing a Web ACL](classic-web-acl-editing.md)\.
**Note**  
When adding a rule group to a web ACL, the action that you set for the rule group \(either **No override** or **Override to count**\) is called the rule group override action\. For more information, see [Rule group override](#classic-waf-managed-rule-group-override)\.<a name="classic-waf-managed-rule-group-unsubscribe-procedure"></a>

**To unsubscribe from an AWS marketplace rule group**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. Remove the rule group from all web ACLs\. For more information, see [Editing a Web ACL](classic-web-acl-editing.md)\.

1. In the navigation pane, choose **Marketplace**\.

1. Choose **Manage your subscriptions**\.

1. Choose **Cancel subscription** next to the name of the rule group that you want to unsubscribe from\.

1. Choose **Yes, cancel subscription**\.<a name="classic-waf-managed-rule-group-exclude-rule-procedure"></a>

**To exclude a rule from a rule group \(rule group exception\)**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. If not already enabled, enable AWS WAF Classic logging\. For more information, see [Logging Web ACL traffic information](classic-logging.md)\. Use the AWS WAF Classic logs to identify the IDs of the rules that you want to exclude\. These are typically rules that are blocking legitimate requests\.

1. In the navigation pane, choose **Web ACLs**\.

1. Choose the web ACL that you want to edit\.
**Note**  
The rule group that you want to edit must be associated with a web ACL before you can exclude a rule from that rule group\.

1. On the **Rules** tab in the right pane, choose **Edit web ACL**\.

1. In the **Rule group exceptions** section, expand the rule group that you want to edit\.

1. Choose the **X** next to the rule that you want to exclude\. You can identify the correct rule ID by using the AWS WAF Classic logs\.

1. Choose **Update**\.

   Excluding rules does not remove those rules from the rule group\. Rather, it changes the action for the rules to `COUNT`\. Therefore, requests that match an excluded rule are counted but not blocked\. You will receive `COUNT` metrics for each excluded rule\.
**Note**  
You can use this same procedure to exclude rules from custom rule groups that you have created in AWS Firewall Manager\. However, rather than excluding a rule from a custom rule group using these steps, you can also simply edit a custom rule group using the steps described in [Adding and deleting rules from an AWS WAF Classic rule group](classic-rule-group-editing.md)\.

## Rule group override<a name="classic-waf-managed-rule-group-override"></a>

AWS Marketplace rule groups have two possible actions: **No override** and **Override to count**\. If you want to test the rule group, set the action to **Override to count**\. This rule group action overrides any *block* action that is specified by individual rules contained within the group\. That is, if the rule group's action is set to **Override to count**, instead of potentially blocking matching requests based on the action of individual rules within the group, those requests will be counted\. Conversely, if you set the rule group's action to **No override**, actions of the individual rules within the group will be used\.

## Troubleshooting AWS marketplace rule groups<a name="classic-waf-managed-rule-group-troubleshooting"></a>

If you find that an AWS Marketplace rule group is blocking legitimate traffic, perform the following steps\.<a name="classic-waf-managed-rule-group-troubleshooting-procedure"></a>

**To troubleshoot an AWS marketplace rule group**

1. Exclude the specific rules that are blocking legitimate traffic\. You can identify which rules are blocking which requests using the AWS WAF Classic logs\. For more information about excluding rules, see [To exclude a rule from a rule group \(rule group exception\)](#classic-waf-managed-rule-group-exclude-rule-procedure)\.

1. If excluding specific rules does not solve the problem, you can change the action for the AWS Marketplace rule group from **No override** to **Override to count**\. This allows the web request to pass through, regardless of the individual rule actions within the rule group\. This also provides you with Amazon CloudWatch metrics for the rule group\.

1. After setting the AWS Marketplace rule group action to **Override to count**, contact the rule group provider‘s customer support team to further troubleshoot the issue\. For contact information, see the rule group listing on the product listing pages on AWS Marketplace\.

### Contacting customer support<a name="classic-waf-managed-rule-group-troubleshooting-support"></a>

For problems with AWS WAF Classic or a rule group that is managed by AWS, contact AWS Support\. For problems with a rule group that is managed by an AWS partner, contact that partner's customer support team\. To find partner contact information, see the partner’s listing on AWS Marketplace\.

## Creating and selling AWS marketplace rule groups<a name="classic-waf-managed-rule-group-creating"></a>

If you want to sell AWS Marketplace rule groups on AWS Marketplace, see [How to Sell Your Software on AWS Marketplace](https://aws.amazon.com/marketplace/management/tour/)\.