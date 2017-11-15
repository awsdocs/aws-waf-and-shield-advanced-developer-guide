# Tutorials<a name="tutorials"></a>

This section contains a link to a preconfigured template as well as three tutorials that present complete solutions for common tasks that you can perform in AWS WAF\. The tutorials show how to combine several AWS services to automatically configure AWS WAF in response to your CloudFront traffic\. Their purpose is to provide general guidance\. They are not intended for direct use in your production environment without careful review and adaptation to the unique aspects of your business environment\.

**AWS WAF Preconfigured Protections**

You can use our preconfigured template to get started quickly with AWS WAF\. The template includes a set of AWS WAF rules that are designed to block common web\-based attacks\. You can customize the template to fit your business needs\. 

The rules in the template help protect against bad bots, SQL injection, cross\-site scripting \(XSS\), HTTP floods, and other known attacks\. After you deploy the template, AWS WAF begins to block the web requests to your CloudFront distributions or Application Load Balancers that match the preconfigured rules in your web access control \(web ACL\) list\. You can use this automated solution in addition to other web ACLs that you configure\. For more information, see [AWS WAF Security Automations](https://aws.amazon.com/answers/security/aws-waf-security-automations/)\.

**Tutorials**

+ [Tutorial: Quickly Setting Up AWS WAF Protection Against Common Attacks](tutorials-common-attacks.md)

+ [Tutorial: Blocking IP Addresses That Submit Bad Requests](tutorials-4xx-blocking.md)

+ [Tutorial: Implementing a DDoS\-resistant Website Using AWS Services](tutorials-ddos-cross-service.md)