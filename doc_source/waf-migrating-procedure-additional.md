# Migrating a web ACL: additional considerations<a name="waf-migrating-procedure-additional"></a>

Review your new web ACL and consider the options available to you in the new AWS WAF to be sure that the configuration is as efficient as possible and that it's using the latest available security options\. 

**Additional AWS Managed Rules**  
Consider implementing additional AWS Managed Rules in your web ACL to increase the security posture for your application\. These are included with AWS WAF at no additional cost\. AWS Managed Rules feature the following types of rule groups: 
+ Baseline rule groups provide general protection against a variety of common threats, such as stopping known bad inputs from making it into your application and preventing admin page access\. 
+ Use\-case specific rule groups provide incremental protection for many diverse use cases and environments\.
+ IP reputation lists provide threat intelligence based on the client’s source IP\.

For more information, see [AWS Managed Rules for AWS WAF](aws-managed-rule-groups.md)\.

**Rule optimization and cleanup**  
Revisit your old rules and consider optimizing them by rewriting them or removing outdated ones\. For example, if in the past, you deployed an AWS CloudFormation template from the technical paper for OWASP Top 10 Web Application Vulnerabilities, [Prepare for the OWASP Top 10 Web Application Vulnerabilities Using AWS WAF and Our New White Paper](https://aws.amazon.com/blogs/aws/prepare-for-the-owasp-top-10-web-application-vulnerabilities-using-aws-waf-and-our-new-white-paper/), you should consider replacing that with AWS Managed Rules\. While the concept found within the document is still applicable and may assist you in writing your own rules, the rules created by the template have been largely superseded by AWS Managed Rules\.

**Amazon CloudWatch metrics and alarms**  
Revisit your Amazon CloudWatch metrics and set up alarms as needed\. The migration doesn't carry over CloudWatch alarms and it's possible that your metric names aren't what you want\. 

**Review with your application team**  
Work with your application team and check your security posture\. Find out what fields are parsed frequently by the application and add rules to sanitize the input accordingly\. Check for any edge cases and add rules to catch these cases if the application’s business logic fails to process them\. 

**Plan the switchover**  
Plan the timing of the switch with your application team\. The switch from the old web ACL association to the new one can cause a brief disruption\. 

When you are ready to switch over, follow the procedure at [Migrating a web ACL: switchover](waf-migrating-procedure-switchover.md)\.