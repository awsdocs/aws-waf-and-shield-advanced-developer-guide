# Creating a Regex Pattern IP Set<a name="waf-regex-pattern-set-creating"></a>

Follow the procedure in this section to create a new regex pattern set\.

**To create a regex pattern set**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Regex pattern sets** and then **Create regex pattern set**\. 

1. Enter a name and description for the regex pattern set\. You'll use these to identify it when you want to use the set\. 
**Note**  
You can't change the name after you create the regex pattern set\.

1. For **Region**, choose the Region where you want to store the regex pattern set\. To use a regex pattern set in web ACLs that protect Amazon CloudFront distributions, you must choose **US East \(N\. Virginia\)**\. You can use the global setting for regional applications too\.

1. In the **Regular expressions** text box, enter one regex pattern per line\. 

   Here are some examples:
   + To specify the IPv4 address 192\.0\.2\.44, type **192\.0\.2\.44/32**\.
   + To specify the IPv6 address 0:0:0:0:0:ffff:c000:22c, type **0:0:0:0:0:ffff:c000:22c/128**\.
   + To specify the range of IPv4 addresses from 192\.0\.2\.0 to 192\.0\.2\.255, type **192\.0\.2\.0/24**\.
   + To specify the range of IPv6 addresses from 2620:0:2d0:200:0:0:0:0 to 2620:0:2d0:200:ffff:ffff:ffff:ffff, enter **2620:0:2d0:200::/64**\.

**Regex pattern use limitations**  
AWS WAF supports [standard Perl Compatible Regular Expressions \(PCRE\)](http://www.pcre.org/) with the following exceptions, which it doesn't support: 
   + Backreferences and capturing subexpressions
   + Arbitrary zero\-width assertions
   + Subroutine references and recursive patterns
   + Conditional patterns
   + Backtracking control verbs
   + The \\C single\-byte directive
   + The \\R newline match directive
   + The \\K start of match reset directive
   + Callouts and embedded code
   + Atomic grouping and possessive quantifiers

1. Review the settings for the regex pattern set, and choose **Create regex pattern set**\.