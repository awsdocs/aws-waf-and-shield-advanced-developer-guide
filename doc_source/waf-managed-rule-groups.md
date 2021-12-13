# Managed rule groups<a name="waf-managed-rule-groups"></a>

Managed rule groups are collections of predefined, ready\-to\-use rules that AWS and AWS Marketplace sellers write and maintain for you:
+ *AWS Managed Rules rule groups* are mostly available for free to AWS WAF customers\. The AWS WAF Bot Control rule group has additional fees\. For more information, see [AWS WAF Pricing](http://aws.amazon.com/waf/pricing/)\.
+ *AWS Marketplace managed rule groups* are available by subscription through AWS Marketplace\.

Some managed rule groups are designed to help protect specific types of web applications like WordPress, Joomla, or PHP\. Others offer broad protection against known threats or common web application vulnerabilities, such as those listed in the [OWASP Top 10](https://owasp.org/www-project-top-ten/)\. If you're subject to regulatory compliance like PCI or HIPAA, you might be able to use managed rule groups to satisfy web application firewall requirements\.

**Automatic updates**  
Keeping up to date on the constantly changing threat landscape can be time consuming and expensive\. Managed rule groups can save you time when you implement and use AWS WAF\. AWS and AWS Marketplace sellers automatically update managed rule groups and provide new versions of rule groups when new vulnerabilities and threats emerge\. 

In some cases, AWS is notified of new vulnerabilities before public disclosure, due to its participation in a number of private disclosure communities\. In those cases, AWS can update the AWS Managed Rules rule groups and deploy them for you even before a new threat is widely known\. 

**Restricted access to rules in a managed rule group**  
Each managed rule group provides a comprehensive description of the types of attacks and vulnerabilities that it's designed to protect against\. To protect the intellectual property of the rule group providers, you can't view details for the individual rules within a rule group\. This restriction also helps to keep malicious users from designing threats that specifically circumvent published rules\.

**Topics**
+ [Version management with managed rule groups](waf-managed-rule-groups-versioning.md)
+ [Working with managed rule groups](waf-using-managed-rule-groups.md)
+ [AWS Managed Rules for AWS WAF](aws-managed-rule-groups.md)
+ [AWS Marketplace managed rule groups](marketplace-managed-rule-groups.md)