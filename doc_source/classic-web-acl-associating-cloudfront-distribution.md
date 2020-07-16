# Associating or disassociating a Web ACL with an Amazon API Gateway API, a CloudFront distribution or an Application Load Balancer<a name="classic-web-acl-associating-cloudfront-distribution"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

To associate or disassociate a web ACL, perform the applicable procedure\. Note that you also can associate a web ACL with a CloudFront distribution when you create or update the distribution\. For more information, see [Using AWS WAF Classic to Control Access to Your Content](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-awswaf.html) in the *Amazon CloudFront Developer Guide*\.

The following restrictions apply when associating a web ACL:
+ Each API Gateway API, Application Load Balancer and CloudFront distribution can be associated with only one web ACL\.
+ Web ACLs associated with a CloudFront distribution cannot be associated with an Application Load Balancer or API Gateway API\. The web ACL can, however, be associated with other CloudFront distributions\.

**To associate a web ACL with an API Gateway API, CloudFront distribution or Application Load Balancer**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Web ACLs**\.

1. Choose the web ACL that you want to associate with an API Gateway API, CloudFront distribution or Application Load Balancer\. 

1. On the **Rules** tab, under **AWS resources using this web ACL**, choose **Add association**\.

1. When prompted, use the **Resource** list to choose the API Gateway API, CloudFront distribution or Application Load Balancer that you want to associate this web ACL with\. If you choose an Application Load Balancer, you also must specify a Region\.

1. Choose **Add**\.

1. To associate this web ACL with an additional API Gateway API, CloudFront distribution or another Application Load Balancer, repeat steps 4 through 6\.<a name="classic-web-acl-disassociating-cloudfront-distribution-procedure"></a>

**To disassociate a web ACL from an API Gateway API, CloudFront distribution or Application Load Balancer**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Web ACLs**\.

1. Choose the web ACL that you want to disassociate from an API Gateway API, CloudFront distribution or Application Load Balancer\.

1. On the **Rules** tab, under **AWS resources using this web ACL**, choose the **x** for each API Gateway API, CloudFront distribution or Application Load Balancer that you want to disassociate this web ACL from\.