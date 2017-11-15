# Deciding on the Default Action for a Web ACL<a name="web-acl-default-action"></a>

When you create and configure a web ACL, the first and most important decision that you must make is whether the default action should be for AWS WAF to allow web requests or to block web requests\. The default action indicates what you want AWS WAF to do after it inspects a web request for all the conditions that you specify, and the web request doesn't match any of those conditions:

+ **Allow** – If you want to allow most users to access your website, but you want to block access to attackers whose requests originate from specified IP addresses, or whose requests appear to contain malicious SQL code or specified values, choose **Allow** for the default action\.

+ **Block** – If you want to prevent most would\-be users from accessing your website, but you want to allow access to users whose requests originate from specified IP addresses, or whose requests contain specified values, choose **Block** for the default action\.

Many decisions that you make after you've decided on a default action depend on whether you want to allow or block most web requests\. For example, if you want to *allow* most requests, then the match conditions that you create generally should specify the web requests that you want to *block*, such as the following:

+ Requests that originate from IP addresses that are making an unreasonable number of requests

+ Requests that originate from countries that either you don't do business in or are the frequent source of attacks

+ Requests that include fake values in the **User\-Agent** header

+ Requests that appear to include malicious SQL code