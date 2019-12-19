# Creating and Managing a Regex Pattern Set<a name="waf-regex-pattern-set-managing"></a>

A regex pattern set provides a collection of regular expressions that you want to use together in a rule statement\. Regex pattern sets are AWS resources\. 

To use a regex pattern set in a web ACL or rule group, you first create an AWS resource, `RegexPatternSet` with your address specifications\. Then you reference the set when you add a regex pattern set rule statement to a web ACL or rule group\. 

If your regex pattern set contains more than one regex pattern, when it's used in a rule, the pattern matching is combined with an *OR*\. That is, a web request will match the pattern set rule statement if the request component matches any of the patterns in the set\.

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

**Topics**
+ [Creating a Regex Pattern IP Set](waf-regex-pattern-set-creating.md)
+ [Using a Regex Pattern Set in a Rule Group or Web ACL](waf-regex-pattern-set-using.md)
+ [Deleting a Regex Pattern Set](waf-regex-pattern-set-deleting.md)