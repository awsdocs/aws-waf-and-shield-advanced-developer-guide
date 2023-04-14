# Associating or disassociating a web ACL with an AWS resource<a name="web-acl-associating-aws-resource"></a>

You can use AWS WAF to create the following associations between web ACLS and your resources: 
+ Associate a regional web ACL with any of the regional resources listed below\. For this option, the web ACL must be in the same region as your resource\. 
  + Amazon API Gateway REST API
  + Application Load Balancer
  + AWS AppSync GraphQL API
  + Amazon Cognito user pool
  + AWS App Runner service
+ Associate a global web ACL with a Amazon CloudFront distribution\. The global web ACL will have a hard\-coded Region of US East \(N\. Virginia\) Region\.

You can also associate a web ACL with a CloudFront distribution when you create or update the distribution itself\. For information, see [Using AWS WAF to Control Access to Your Content](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-awswaf.html) in the *Amazon CloudFront Developer Guide*\.

**Restrictions on multiple associations**  
You can associate a single web ACL with one or more AWS resources, according to the following restrictions:
+ You can associate each AWS resource with only one web ACL\. The relationship between web ACL and AWS resources is one\-to\-many\. 
+ You can associate a web ACL with one or more CloudFront distributions\. You cannot associate a web ACL that you have associated with a CloudFront distribution with any other AWS resource type\.

**Additional restrictions**  
The following additional restrictions apply to web ACL associations: 
+ You can only associate a web ACL to an Application Load Balancer within AWS Regions\. For example, you cannot associate a web ACL to an Application Load Balancer that is on AWS Outposts\.
+ You can't associate an Amazon Cognito user pool with a web ACL that uses the AWS WAF Fraud Control account takeover prevention \(ATP\) managed rule group `AWSManagedRulesATPRuleSet`\. For information about account takeover prevention, see [AWS WAF Fraud Control account takeover prevention \(ATP\)](waf-atp.md)\. 

**Production traffic risk**  
Before you deploy your web ACL for production traffic, test and tune it in a staging or testing environment until you are comfortable with the potential impact to your traffic\. Then test and tune your rules in count mode with your production traffic before enabling them\. For guidance, see [Testing and tuning your AWS WAF protections](web-acl-testing.md)\.

**To associate a web ACL with an AWS resource**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Web ACLs**\.

1. Choose the name of the web ACL that you want to associate with a resource\. The console takes you to the web ACL's description, where you can edit it\.

1. On the **Associated AWS resources** tab, choose **Add AWS resources**\.

1. When prompted, choose the resource type, select the radio button next to the resource that you want to associate, and then choose **Add**\. 

**To disassociate a web ACL from an AWS resource**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Web ACLs**\.

1. Choose the name of the web ACL that you want to disassociate from your resource\. The console takes you to the web ACL's description, where you can edit it\.

1. On the **Associated AWS resources** tab, select the resource that you want to disassociate this web ACL from and then choose **Disassociate**\. The console opens a confirmation dialogue\. Confirm your choice to disassociate the web ACL from the AWS resource\. 