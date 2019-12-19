# Step 5: Deploy AWS WAF Classic Rules<a name="get-started-fms-shield-deploy-waf-automations"></a>

Several resources are available to help you quickly deploy AWS WAF Classic rules\. Consider taking advantage of one or more of the following offerings when creating your initial set of rules\. You can then use these rules to set up a Firewall Manager\-AWS WAF policy, as described in [Working with AWS Firewall Manager Policies](working-with-policies.md)\. 

**Security automation templates**  
AWS provides preconfigured templates that include a set of AWS WAF Classic rules, which you can customize to best fit your needs\. These templates are designed to block common web\-based attacks such as bad bots, SQL injection, cross\-site scripting \(XSS\), HTTP floods, and known\-attacker attacks\. In addition to activating Shield Advanced and specifying resources for Shield Advanced protection, you also should use these preconfigured templates\.   
For more information, see [AWS WAF Security Automations](https://aws.amazon.com/answers/security/aws-waf-security-automations/)\. AWS WAF is included with Shield Advanced at no additional cost\. 

**AWS Marketplace rule groups**  
AWS WAF provides *AWS Marketplace rule groups* to help you protect your resources\. AWS Marketplace rule groups are collections of predefined, ready\-to\-use rules that are written and updated by AWS and AWS Marketplace sellers\. For more information, see [Managed Rule Groups](waf-managed-rule-groups.md)\.

**AWS WAF for OWASP Top 10 Web Application Vulnerabilities**  
This document outlines how you can use AWS WAF to mitigate the application vulnerabilities that are defined in the Open Web Application Security Project \(OWASP\) Top 10 list\. This list shows the most common categories of application security flaws\. For more information, see [AWS WAF Security Automations](https://d0.awsstatic.com/whitepapers/Security/aws-waf-owasp.pdf)\. 

As a final step for getting started with Firewall Manager and Shield Advanced, review the global threat environment dashboard, as described in [Step 6: Monitor the Global Threat Environment Dashboard ](get-started-fms-shield-monitor-global-dashboard.md)\.