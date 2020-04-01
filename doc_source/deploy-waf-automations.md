# Step 6: Deploy AWS WAF rules<a name="deploy-waf-automations"></a>

Several resources are available to help you quickly deploy AWS WAF rules\. Consider taking advantage of one or more of the following offerings when creating your initial set of rules:

**Security automation templates**  
AWS provides preconfigured templates that include a set of AWS WAF rules, which you can customize to best fit your needs\. These templates are designed to block common web\-based attacks such as bad bots, SQL injection, cross\-site scripting \(XSS\), HTTP floods, and known\-attacker attacks\. In addition to activating Shield Advanced and specifying resources for Shield Advanced protection, you also should use these preconfigured templates\.   
For more information, see [AWS WAF Security Automations](https://aws.amazon.com/solutions/aws-waf-security-automations/)\. AWS WAF is included with Shield Advanced at no additional cost\. 

**AWS Marketplace rule groups**  
AWS WAF provides *AWS Marketplace rule groups* to help you protect your resources\. AWS Marketplace rule groups are collections of predefined, ready\-to\-use rules that are written and updated by AWS and AWS Marketplace sellers\. For more information, see [Managed rule groups](waf-managed-rule-groups.md)\.

**AWS WAF for OWASP Top 10 Web Application Vulnerabilities**  
This document outlines how you can use AWS WAF to mitigate the application vulnerabilities that are defined in the Open Web Application Security Project \(OWASP\) Top 10 list\. This list shows the most common categories of application security flaws\. For more information, see [AWS WAF Security Automations](https://d0.awsstatic.com/whitepapers/Security/aws-waf-owasp.pdf)\. 

**Managed Rules**  
AWS provides managed rules to customers of AWS WAF who are subscribed to AWS Shield Advanced\. These rules are written by the AWS Threat Research Team \(TRT\)\. They help protect against exploitation of a wide range of vulnerabilities, including those described in OWASP publications and many Common Vulnerabilities and Exposures \(CVE\)\. They also provide IP reputation rules that use threat intelligence from Amazon to block known malicious sources\. You do not have to take any action to receive automatic updates to managed rules\.   
To request managed rules, open an “AWS Shield” case in the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\. To learn more about opening an AWS support case, see [Getting Started with AWS Support](https://docs.aws.amazon.com/awssupport/latest/user/getting-started.html)\. 

As a final step for getting started with Shield Advanced, review the global threat environment dashboard, as described in [Step 7: Monitor the global threat environment dashboard ](monitor-global-dashboard.md)\.