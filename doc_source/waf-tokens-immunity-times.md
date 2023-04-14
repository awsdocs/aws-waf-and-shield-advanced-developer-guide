# Timestamp expiration: token immunity times<a name="waf-tokens-immunity-times"></a>

AWS WAF uses challenge and CAPTCHA immunity times to control how frequently a single client session can be presented with a challenge or CAPTCHA\. After an end user successfully responds to a CAPTCHA, the CAPTCHA immunity time determines how long the end user remains immune from being presented with another CAPTCHA\. Similarly, the challenge immunity time determines how long a client session remains immune from being challenged again after successfully responding to a challenge\. 

AWS WAF records a successful response to a challenge or CAPTCHA by updating the corresponding timestamp inside the token\. When AWS WAF inspects the token for challenge or CAPTCHA, it subtracts the timestamp from the current time\. If the result is greater than the configured immunity time, the timestamp is expired\. 

You can configure the challenge and CAPTCHA immunity times in the web ACL and also in any rule that uses the CAPTCHA or Challenge rule action\. 
+ The default web ACL setting for both immunity times is 300 seconds\. 
+ You can specify the immunity time for any rule that uses the CAPTCHA or Challenge action\. If you don't specify the immunity time for the rule, it inherits the setting from the web ACL\. 
+ For a rule inside a rule group that uses the CAPTCHA or Challenge action, if you don't specify the immunity time for the rule, it will inherit the setting from each web ACL where you use the rule group\.
+ The application integration SDKs use the web ACL's challenge immunity time\. 

The minimum value for the challenge immunity time is 300 seconds\. The minimum value for the CAPTCHA immunity time is 60 seconds\. The maximum value for both immunity times is 259,200 seconds, or three days\. 

You can use the web ACL and rule level immunity time settings to tune the CAPTCHA action, Challenge, or SDK challenge management behavior\. For example, you might configure rules that control access to highly sensitive data with low immunity times, and then set higher immunity times in your web ACL for your other rules and the SDKs to inherit\. 

In particular for CAPTCHA, solving a puzzle can degrade your customer's website experience, so tuning the CAPTCHA immunity time can help you mitigate the impact on customer experience while still providing the protections that you want\. 

For additional information about tuning the immunity times for your use of the Challenge and CAPTCHA rule actions, see [Best practices for using the CAPTCHA and Challenge actions](waf-captcha-and-challenge-best-practices.md)\.