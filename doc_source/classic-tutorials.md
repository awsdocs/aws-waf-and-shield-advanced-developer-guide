# Tutorials for AWS WAF Classic<a name="classic-tutorials"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

This section contains a link to a preconfigured template as well as three tutorials that present complete solutions for common tasks that you can perform in AWS WAF Classic\. The tutorials show how to combine several AWS services to automatically configure AWS WAF Classic in response to your CloudFront traffic\. Their purpose is to provide general guidance\. They are not intended for direct use in your production environment without careful review and adaptation to the unique aspects of your business environment\.

**AWS WAF Classic Preconfigured Protections**

You can use our preconfigured template to get started quickly with AWS WAF Classic\. The template includes a set of AWS WAF Classic rules that are designed to block common web\-based attacks\. You can customize the template to fit your business needs\. 

The rules in the template help protect against bad bots, SQL injection, cross\-site scripting \(XSS\), HTTP floods, and other known attacks\. After you deploy the template, AWS WAF Classic begins to block the web requests to your CloudFront distribution or to an Application Load Balancer that matches the preconfigured rules in your web access control \(web ACL\) list\. You can use this automated solution in addition to other web ACLs that you configure\. For more information, see [AWS WAF Classic Security Automations](https://aws.amazon.com/answers/security/aws-waf-security-automations/)\.

**Tutorials for AWS WAF Classic**
+ [Tutorial: Quickly setting up AWS WAF Classic protection against common attacks](classic-tutorials-common-attacks.md)
+ [Tutorial: Implementing a DDoS\-resistant website using AWS services](classic-tutorials-ddos-cross-service.md)