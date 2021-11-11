# Best practices for using AWS WAF CAPTCHA<a name="waf-captcha-best-practices"></a>

Follow the guidance in this section to plan and implement AWS WAF CAPTCHA\.

**Plan your CAPTCHA implementation**  
Determine where to place CAPTCHA challenges based on your website usage and the sensitivity of the data that you want to protect\. Select the requests where you'll use CAPTCHA so that you present challenges as needed, but avoid presenting challenges where they wouldn't be useful and might degrade user experience\. 

Identify the requests that you don't want to have impacted by CAPTCHA, for example, requests for CSS or images\. Avoid using CAPTCHA unnecessarily\. For example, if you plan to have a CAPTCHA check at login, and the user is always taken directly from the login to another screen, requiring a CAPTCHA check at the second screen would probably not be needed\. 

**Protect your sensitive non\-HTML data with CAPTCHA**  
You can use CAPTCHA protections for sensitive non\-HTML data, like APIs, with the following approach\. 

1. Identify requests that take HTML responses and that are run in close proximity to the requests for your sensitive, non\-HTML data\. 

1. Write CAPTCHA rules that match against the requests for HTML and that match against the requests for your sensitive data\. 

1. Tune your CAPTCHA immunity time settings so that, for normal user interactions, the CAPTCHA tokens that clients obtain from the HTML requests are available and unexpired in their requests for your sensitive data\. 

When a request for your sensitive data matches a CAPTCHA rule, it won't be blocked if the client still has the valid token from a prior challenge\. If the token isn't available or is expired, the request to access your sensitive data will fail\. For more information about how the CAPTCHA rule action works, see [CAPTCHA action behavior](waf-captcha-how-it-works.md#waf-captcha-action)\.

**Use CAPTCHA to tune your existing rules**  
Review your existing rules, to see if you want to alter or add to them\. The following are some common scenarios to consider\. 
+ If you have a rate\-based rule that blocks traffic, but you keep the rate limit relatively high to avoid blocking legitimate users, consider adding a second rate\-based rule, before the blocking rule, that has a lower limit and CAPTCHA action\. This way the blocking rule would still block any IP from sending requests at too high a rate\. The CAPTCHA rule would block most automated traffic at an even lower rate\. For information about rate\-based rules, see [Rate\-based rule statement](waf-rule-statement-type-rate-based.md)\.
+ If you have a managed rule group that uses labeling and that blocks requests, you can switch the behavior for some or all of the rules from Block to CAPTCHA\. To do this, in the managed rule group configuration, set the rules that you want to use with CAPTCHA to count\. Then, add a rule to run after the managed rule group that matches against the labels from the managed rule group, and set this rule action to CAPTCHA\. For information about labeling, see [AWS WAF labels on web requests](waf-rule-labels.md)\. For information about setting rules to count, see [Setting the rule actions to count](web-acl-rule-group-override-options.md#web-acl-rule-group-override-options-rules)\. 

**Test your CAPTCHA implementation before you deploy it**  
Follow these guidelines to test and deploy AWS WAF CAPTCHA\.

1. As for all changes, add the CAPTCHA rule action to a rule in a web ACL that's only used for a test or staging environment\. Select rules that you can easily test for matching and non\-matching conditions, such as a custom header value or a specific URL\. 

1. Use the AWS WAF Amazon CloudWatch metrics for monitoring CAPTCHA performance\. You can optionally create a dashboard for your CAPTCHA metrics\.

1. Review your expiration requirements and set your web ACL and rule level CAPTCHA immunity time configurations so that you achieve a good balance between controlling access to your website and providing a good experience for your customers\. 

1. After you have sufficient confidence with the expected user experience and traffic impact, consider adding CAPTCHA as an action to a web ACL that's associated with production traffic\. Add the action either in a new rule or in place of an existing rule that currently uses a Block action for a portion of your traffic\. For example, you could choose to add a geographic region based or path\-based condition that historically has a target traffic volume you are comfortable with before enabling everywhere\. 