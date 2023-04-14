# CAPTCHA and Challenge actions in AWS WAF<a name="waf-captcha-and-challenge"></a>

You can configure your AWS WAF rules to run a CAPTCHA or Challenge action against web requests that match your rule's inspection criteria\. 
+ CAPTCHA requires the end user to solve a CAPTCHA puzzle to prove that a human being is sending the request\. 
+ Challenge runs a silent challenge that requires the client session to verify that it's a browser, and not a bot\. The verification runs in the background without involving the end user\. This is a good option for verifying clients that you suspect of being invalid without negatively impacting the end user experience with a CAPTCHA puzzle\. 

  The Challenge rule action is similar to the challenges in the application integration SDKs, described at [AWS WAF client application integration](waf-application-integration.md)\.

**Note**  
You are charged additional fees when you use the CAPTCHA or Challenge rule action in one of your rules or as a rule action override in a rule group\. For more information, see [AWS WAF Pricing](http://aws.amazon.com/waf/pricing/)\.

After the user or client responds successfully, the script running the CAPTCHA or challenge automatically resubmits the original web request with the updated token\. 

For a description of rule action settings, see [AWS WAF rule action](waf-rule-action.md)\. 

**Topics**
+ [What is a CAPTCHA puzzle?](waf-captcha-puzzle.md)
+ [How the CAPTCHA and Challenge actions work](waf-captcha-and-challenge-how-it-works.md)
+ [Best practices for using the CAPTCHA and Challenge actions](waf-captcha-and-challenge-best-practices.md)