# Getting started with AWS Firewall Manager to enable AWS WAF Classic rules<a name="classic-getting-started-fms"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

You can use AWS Firewall Manager to enable AWS WAF rules, AWS WAF Classic rules, AWS Shield Advanced protections, and Amazon VPC security groups\. The steps for getting set up are slightly different for each:
+ To use Firewall Manager to enable rules using the latest version of AWS WAF, don't use this topic\. Instead, follow the steps in [Getting started with AWS Firewall Manager AWS WAF policies](getting-started-fms.md)\. 
+ To use Firewall Manager to enable AWS Shield Advanced protections, follow the steps in [Getting started with AWS Firewall Manager AWS Shield Advanced policies](getting-started-fms-shield.md)\.
+ To use Firewall Manager to enable Amazon VPC security groups, follow the steps in [Getting started with AWS Firewall Manager Amazon VPC security group policies](getting-started-fms-security-group.md)\. 

To use Firewall Manager to enable AWS WAF Classic rules, perform the following steps in sequence\. 

**Topics**
+ [Step 1: Complete the prerequisites](classic-complete-prereq.md)
+ [Step 2: Create rules](classic-get-started-fms-create-rules.md)
+ [Step 3: Create a rule group](classic-get-started-fms-create-rule-group.md)
+ [Step 4: Create and apply an AWS Firewall Manager AWS WAF Classic policy](classic-get-started-fms-create-security-policy.md)