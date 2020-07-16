# Associating or disassociating a Web ACL with an AWS resource<a name="web-acl-associating-aws-resource"></a>

You can use AWS WAF to associate a web ACL with the following AWS regional resource types:
+ Application Load Balancer
+ Amazon API Gateway REST API

You can associate a web ACL with a CloudFront distribution when you create or update the distribution itself\. For information, see [Using AWS WAF to Control Access to Your Content](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-awswaf.html) in the *Amazon CloudFront Developer Guide*\.

You can only associate a web ACL to an Application Load Balancer within AWS Regions\. For example, you can't associate a web ACL to an Application Load Balancer that is on AWS Outposts\.

**Restrictions on multiple associations**  
You can associate a single web ACL with one or more AWS resources, according to the following restrictions:
+ You can associate each AWS resource with only one web ACL\. The relationship between web ACL and AWS resources is one\-to\-many\. 
+ You can associate a web ACL with one or more CloudFront distributions\. You can't associate a web ACL that you've associated with a CloudFront distribution with any other AWS resource type\.

**To associate a web ACL with an Amazon CloudFront distribution, an Amazon API Gateway REST API, or an Application Load Balancer**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Web ACLs**\.

1. Choose the web ACL that you want to associate with a resource\. 

1. On the **Associated AWS resources** tab, choose **Add AWS resources**\.

1. When prompted, choose your resource that you want to associate this web ACL with\. If you choose an Amazon API Gateway REST API or an Application Load Balancer, specify a Region\.

1. Choose **Add**\.<a name="web-acl-disassociating-aws-resource-procedure"></a>

**To disassociate a web ACL from an Amazon CloudFront distribution, an Amazon API Gateway REST API, or an Application Load Balancer**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Web ACLs**\.

1. Choose the web ACL that you want to disassociate from your resource\.

1. On the **Associated AWS resources** tab, deselect the resources that you want to disassociate this web ACL from\.

1. Choose **Save**\.