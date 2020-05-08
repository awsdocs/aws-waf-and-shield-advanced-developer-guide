# Listing IP addresses blocked by rate\-based rules<a name="classic-listing-managed-ips"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

AWS WAF Classic provides a list of IP addresses that are blocked by rate\-based rules\.<a name="classic-listing-managed-ips-procedure"></a>

**To view addresses blocked by rate\-based rules**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Rules**\.

1. In the **Name** column, choose a rate\-based rule\.

   The list shows the IP addresses that the rule currently blocks\.