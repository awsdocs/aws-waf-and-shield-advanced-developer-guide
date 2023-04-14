# How the CAPTCHA and Challenge actions work<a name="waf-captcha-and-challenge-how-it-works"></a>

AWS WAF CAPTCHA and Challenge are standard rule actions, so they're relatively easy to implement\. To use either of them, you create the inspection criteria for your rule that identifies the requests that you want to inspect, and then specify one of the two rule actions\. For general information about rule action options, see [AWS WAF rule action](waf-rule-action.md)\.

**Topics**
+ [CAPTCHA and Challenge action behavior](#waf-captcha-and-challenge-actions)
+ [CAPTCHA and Challenge actions in the logs and metrics](#waf-captcha-and-challenge-logs-metrics)

## CAPTCHA and Challenge action behavior<a name="waf-captcha-and-challenge-actions"></a>

When a web request matches the inspection criteria of a rule with CAPTCHA or Challenge action, AWS WAF determines how to handle the request according to the state of its token and immunity time configuration\. AWS WAF also considers whether the request can handle the CAPTCHA puzzle or challenge script interstitials\. The scripts are designed to be handled as HTML content, and they can only be handled properly by a client that's expecting HTML content\. 

**Note**  
You are charged additional fees when you use the CAPTCHA or Challenge rule action in one of your rules or as a rule action override in a rule group\. For more information, see [AWS WAF Pricing](http://aws.amazon.com/waf/pricing/)\.

**How the action handles the web request**  
AWS WAF applies the CAPTCHA or Challenge action to a web request as follows:
+ **Valid token** – AWS WAF handles this similar to a `Count` action\. AWS WAF applies any labels and request customizations that you've configured for the rule action, and then continues evaluating the request using the remaining rules in the web ACL\. 
+ **Missing, invalid, or expired token** – AWS WAF discontinues the web ACL evaluation of the request and blocks it from going to its intended destination\. 

  AWS WAF generates a response that it sends back to the client, according to the rule action type: 
  + **Challenge** – AWS WAF includes the following in the response:
    + The header `x-amzn-waf-action` with a value of `challenge`\.
    + The HTTP status code `202 Request Accepted`\.
    + If the request contains an `Accept` header with a value of `text/html`, the response includes a JavaScript page interstitial with a challenge script\.
  + **CAPTCHA** – AWS WAF includes the following in the response:
    + The header `x-amzn-waf-action` with a value of `captcha`\.
    + The HTTP status code `405 Method Not Allowed`\.
    + If the request contains an `Accept` header with a value of `text/html`, the response includes a JavaScript page interstitial with a CAPTCHA script\. 

To configure the timing of token expiration at the web ACL or rule level, see [Timestamp expiration: token immunity times](waf-tokens-immunity-times.md)\.

**What the interstitial does**  
When a challenge interstitial runs, after the client responds successfully, if it doesn't already have a token, the interstitial initializes one for it\. Then it updates the token with the challenge solve timestamp\.

When a CAPTCHA interstitial runs, if the client doesn't have a token yet, the CAPTCHA interstitial invokes the challenge script first to challenge the browser and initialize the token\. Then the interstitial runs its CAPTCHA puzzle\. When the end user successfully completes the puzzle, the interstitial updates the token with the CAPTCHA solve timestamp\. 

In either case, after the client responds successfully and the script updates the token, the script resubmits the original web request using the updated token\. 

You can configure how AWS WAF handles tokens\. For information, see [AWS WAF web request tokens](waf-tokens.md)\.

## CAPTCHA and Challenge actions in the logs and metrics<a name="waf-captcha-and-challenge-logs-metrics"></a>

The CAPTCHA and Challenge actions can be non\-terminating, like `Count`, or terminating, like `Block`\. The outcome depends on whether the request has a valid token with an unexpired timestamp for the action type\. 
+ **Valid token** – When the action finds a valid token and doesn't block the request, AWS WAF captures metrics and logs as follows:
  + Increments the metrics for either `CaptchaRequests` and `RequestsWithValidCaptchaToken` or `ChallengeRequests` and `RequestsWithValidChallengeToken`\. 
  + Logs the match as a `nonTerminatingMatchingRules` entry with action of CAPTCHA or Challenge\. The following listing shows the section of a log for this type of match with the CAPTCHA action\.

    ```
        "nonTerminatingMatchingRules": [
        {
          "ruleId": "captcha-rule",
          "action": "CAPTCHA",
          "ruleMatchDetails": [],
          "captchaResponse": {
            "responseCode": 0,
            "solveTimestamp": 1632420429
          }
        }
      ]
    ```
+ **Missing, invalid, or expired token** – When the action blocks the request due to a missing or invalid token, AWS WAF captures metrics and logs as follows:
  + Increments the metric for `CaptchaRequests` or `ChallengeRequests`\. 
  + Logs the match as a `CaptchaResponse` entry with HTTP `405` status code or as a `ChallengeResponse` entry with HTTP `202` status code\. The log indicates whether the request was missing the token or had an expired timestamp\. The log also indicates whether AWS WAF sent a CAPTCHA interstitial page to the client or a silent challenge to the client browser\. The following listing shows the sections of a log for this type of match with the CAPTCHA action\.

    ```
        "terminatingRuleId": "captcha-rule",
        "terminatingRuleType": "REGULAR",
        "action": "CAPTCHA",
        "terminatingRuleMatchDetails": [],
        ...
        "responseCodeSent": 405,
        ...
        "captchaResponse": {
          "responseCode": 405,
          "solveTimestamp": 0,
          "failureReason": "TOKEN_MISSING"
        }
    ```

For information about the AWS WAF logs, see [Logging web ACL traffic](logging.md)\.

For information about AWS WAF metrics, see [AWS WAF metrics and dimensions](monitoring-cloudwatch.md#waf-metrics)\.

For information about rule action options, see [AWS WAF rule action](waf-rule-action.md)\.