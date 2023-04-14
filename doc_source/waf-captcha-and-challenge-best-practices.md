# Best practices for using the CAPTCHA and Challenge actions<a name="waf-captcha-and-challenge-best-practices"></a>

Follow the guidance in this section to plan and implement AWS WAF CAPTCHA or challenge\.

**Plan your CAPTCHA and challenge implementation**  
Determine where to place CAPTCHA puzzles or silent challenges based on your website usage, the sensitivity of the data that you want to protect, and the type of requests\. Select the requests where you'll apply CAPTCHA so that you present the puzzles as needed, but avoid presenting them where they wouldn't be useful and might degrade the user experience\. Use the Challenge action to run silent challenges that have less impact on the end user, but still help verify that the request is coming from a JavaScript enabled browser\. 

Identify requests that you don't want to have impacted by CAPTCHA, for example, requests for CSS or images\. Use CAPTCHA only when necessary\. For example, if you plan to have a CAPTCHA check at login, and the user is always taken directly from the login to another screen, requiring a CAPTCHA check at the second screen would probably not be needed and might degrade your end user experience\. 

Use the Challenge and CAPTCHA actions only on `GET` `text/html` requests\. Don't use them for `POST` or other request types, because browser behavior for other requests can vary and might not be able to handle the interstitials properly\. 

It's possible for a client to accept HTML but still not be able to handle the CAPTCHA or challenge interstitial\. For example, a widget on a webpage with a small iFrame might accept HTML but not be able to display a CAPTCHA or process it\. Avoid placing the rule actions for these types of requests, the same as for requests that don't accept HTML\.

**How to protect your sensitive non\-HTML data with CAPTCHA and Challenge**  
You can use CAPTCHA and Challenge protections for sensitive non\-HTML data, like APIs, with the following approach\. 

1. Identify requests that take HTML responses and that are run in close proximity to the requests for your sensitive, non\-HTML data\. 

1. Write CAPTCHA or Challenge rules that match against the requests for HTML and that match against the requests for your sensitive data\. 

1. Tune your CAPTCHA and Challenge immunity time settings so that, for normal user interactions, the tokens that clients obtain from the HTML requests are available and unexpired in their requests for your sensitive data\. For tuning information, see [Timestamp expiration: token immunity times](waf-tokens-immunity-times.md)\.

When a request for your sensitive data matches a CAPTCHA or Challenge rule, it won't be blocked if the client still has a valid token from the prior puzzle or challenge\. If the token isn't available or the timestamp is expired, the request to access your sensitive data will fail\. For more information about how the rule actions work, see [CAPTCHA and Challenge action behavior](waf-captcha-and-challenge-how-it-works.md#waf-captcha-and-challenge-actions)\.

**Use CAPTCHA and Challenge to tune your existing rules**  
Review your existing rules, to see if you want to alter or add to them\. The following are some common scenarios to consider\. 
+ If you have a rate\-based rule that blocks traffic, but you keep the rate limit relatively high to avoid blocking legitimate users, consider adding a second rate\-based rule, before the blocking rule that has a lower limit and CAPTCHA or Challenge action\. The blocking rule will still block any IP from sending requests at too high a rate, and the new rule will block most automated traffic at an even lower rate\. For information about rate\-based rules, see [Rate\-based rule statement](waf-rule-statement-type-rate-based.md)\.
+ If you have a managed rule group that blocks requests, you can switch the behavior for some or all of the rules from Block to CAPTCHA or Challenge\. To do this, in the managed rule group configuration, override the rule action setting\. For information about overriding rule actions, see [Rule action overrides](web-acl-rule-group-override-options.md#web-acl-rule-group-override-options-rules)\. 

**Test your CAPTCHA and challenge implementations before you deploy them**  
As for all new functionality, follow the guidance at [Testing and tuning your AWS WAF protections](web-acl-testing.md)\.

During testing, review your token timestamp expiration requirements and set your web ACL and rule level immunity time configurations so that you achieve a good balance between controlling access to your website and providing a good experience for your customers\. For information, see [Timestamp expiration: token immunity times](waf-tokens-immunity-times.md)\.