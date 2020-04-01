# Creating a regex pattern set<a name="waf-regex-pattern-set-creating"></a>

Follow the procedure in this section to create a new regex pattern set\.

**To create a regex pattern set**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Regex pattern sets** and then **Create regex pattern set**\. 

1. Enter a name and description for the regex pattern set\. You'll use these to identify it when you want to use the set\. 
**Note**  
You can't change the name after you create the regex pattern set\.

1. For **Region**, choose the Region where you want to store the regex pattern set\. To use a regex pattern set in web ACLs that protect Amazon CloudFront distributions, you must use Global \(CloudFront\)\. 

1. In the **Regular expressions** text box, enter one regex pattern per line\. 

   For example, the regular expression `I[a@]mAB[a@]dRequest` matches the following strings: `IamABadRequest`, `IamAB@dRequest`, `I@mABadRequest`, and `I@mAB@dRequest`\.

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