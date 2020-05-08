# Deleting a Web ACL<a name="classic-web-acl-deleting"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

To delete a web ACL, you must remove the rules that are included in the web ACL and disassociate all CloudFront distributions and Application Load Balancers from the web ACL\. Perform the following procedure\.<a name="classic-web-acl-deleting-procedure"></a>

**To delete a web ACL**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Web ACLs**\.

1. Choose the web ACL that you want to delete\.

1. On the **Rules** tab in the right pane, choose **Edit web ACL**\.

1. To remove all rules from the web ACL, choose the **x** at the right of the row for each rule\. This doesn't delete the rules from AWS WAF Classic, it just removes the rules from this web ACL\.

1. Choose **Update**\.

1. Disassociate the web ACL from all CloudFront distributions and Application Load Balancers\. On the **Rules** tab, under **AWS resources using this web ACL**, choose the **x** for each API Gateway API, CloudFront distribution or Application Load Balancer\.

1. On the **Web ACLs** page, confirm that the web ACL that you want to delete is selected, and then choose **Delete**\.