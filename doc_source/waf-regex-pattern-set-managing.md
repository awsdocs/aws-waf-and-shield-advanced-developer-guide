# Creating and managing a regex pattern set<a name="waf-regex-pattern-set-managing"></a>

A regex pattern set provides a collection of regular expressions that you want to use together in a rule statement\. Regex pattern sets are AWS resources\. 

To use a regex pattern set in a web ACL or rule group, you first create an AWS resource, `RegexPatternSet` with your regex pattern specifications\. Then you reference the set when you add a regex pattern set rule statement to a web ACL or rule group\. A regex pattern set must contain at least one regex pattern\. 

If your regex pattern set contains more than one regex pattern, when it's used in a rule, the pattern matching is combined with an *OR*\. That is, a web request will match the pattern set rule statement if the request component matches any of the patterns in the set\.

AWS WAF supports the pattern syntax used by the PCRE library `libpcre`\. The library is documented at [PCRE \- Perl Compatible Regular Expressions](http://www.pcre.org/)\. 

**Regex pattern use limitations**  
AWS WAF doesn't support all contructs of the library\. For example, it supports some zero\-width assertions, but not all\. We do not have comprehensive list of the constructs that are supported\. However, if you provide a regex pattern that isn't valid or use unsupported constructs, the AWS WAF API reports a failure\. 

AWS WAF does not support the following PCRE patterns: 
+ Backreferences and capturing subexpressions
+ Subroutine references and recursive patterns
+ Conditional patterns
+ Backtracking control verbs
+ The \\C single\-byte directive
+ The \\R newline match directive
+ The \\K start of match reset directive
+ Callouts and embedded code
+ Atomic grouping and possessive quantifiers

**Topics**
+ [Creating a regex pattern set](waf-regex-pattern-set-creating.md)
+ [Using a regex pattern set in a rule group or Web ACL](waf-regex-pattern-set-using.md)
+ [Deleting a regex pattern set](waf-regex-pattern-set-deleting.md)