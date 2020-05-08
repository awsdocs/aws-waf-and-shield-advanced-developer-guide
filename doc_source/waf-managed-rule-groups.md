# Managed rule groups<a name="waf-managed-rule-groups"></a>

Managed rule groups are collections of predefined, ready\-to\-use rules that AWS and AWS Marketplace sellers write and maintain for you:
+ *AWS Managed Rules rule groups* are available for free to AWS WAF customers\. 
+ *AWS Marketplace managed rule groups* are available by subscription through AWS Marketplace\.

Some managed rule groups are designed to help protect specific types of web applications like WordPress, Joomla, or PHP\. Others offer broad protection against known threats or common web application vulnerabilities, such as those listed in the [OWASP Top 10](https://owasp.org/www-project-top-ten/)\. If you're subject to regulatory compliance like PCI or HIPAA, you might be able to use managed rule groups to satisfy web application firewall requirements\.

**Automatic Updates**  
Keeping up to date on the constantly changing threat landscape can be time consuming and expensive\. Managed rule groups can save you time when you implement and use AWS WAF\. AWS and AWS Marketplace sellers automatically update managed rule groups when new vulnerabilities and threats emerge\.

AWS and many of the AWS Marketplace sellers are notified of new vulnerabilities before public disclosure\. AWS WAF can update their rule groups and deploy them to you even before a new threat is widely known\. Many also have threat research teams to investigate and analyze the most recent threats in order to write the most relevant rules\.

**Access to the Rules in a Managed Rule Group**  
Each AWS Marketplace rule group provides a comprehensive description of the types of attacks and vulnerabilities that it's designed to protect against\. To protect the intellectual property of the rule group providers, you can't view the individual rules within a rule group\. This restriction also helps to keep malicious users from designing threats that specifically circumvent published rules\.

You can’t view individual rules in a managed rule group, and you can't edit them\. However, you can exclude specific rules from a rule group when you add it to your web ACL\. You can also override all rule actions in the group to `COUNT`\. For more information, see the following section and also see the steps for adding a managed rule group in the procedure [Creating a web ACL](web-acl-creating.md)\. 

**Topics**
+ [Working with managed rule groups](waf-using-managed-rule-groups.md)
+ [AWS Managed Rules for AWS WAF](aws-managed-rule-groups.md)
+ [AWS Marketplace managed rule groups](marketplace-managed-rule-groups.md)