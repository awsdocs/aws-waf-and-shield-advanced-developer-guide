# Tips for migrating your AWS WAF Classic resources to AWS WAF<a name="waf-migrating-from-classic"></a>

**Note**  
This is the latest version of **AWS WAF**\. If you created AWS WAF resources, like rules and web ACLs, prior to November, 2019, you either need to use AWS WAF Classic to work with those resources, or you need to migrate them to this latest version\. 

This section provides high\-level guidance for migrating your rules and web ACLs from AWS WAF Classic to AWS WAF\. 

**Before you begin**  
Understand the options and expanded capabilities of this latest version of AWS WAF by reading the information in this AWS WAF developer guide\. For example, your options for rules management now include logical AND, OR, and NOT statements and you can nest rules\. AWS WAF support full CIDR notation in IP address specifications\. 

Additionally, AWS WAF now provides a set of rule groups for your use, free of charge\. You might want to use these in your new web ACL configurations, in place of some of your prior settings\. For information, see [Managed rule groups](waf-managed-rule-groups.md)\. 

**General steps to migrate your web ACLs from AWS WAF Classic to AWS WAF**  
For each web ACL that you use in AWS WAF Classic, do the following:

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

   Choose **Switch to AWS WAF Classic** and review your configuration settings for the web ACL\. Make note of the settings that you want to migrate for the web ACL\. This is a manual process\.

1. In another browser session, follow the guidance at [Creating a web ACL](web-acl-creating.md) to create a web ACL in AWS WAF that's based on your AWS WAF Classic web ACL\. 

1. In AWS WAF Classic, disassociate old web ACL from your AWS resources\. 

1. In AWS WAF, associate the new web ACL with your AWS resources\. 