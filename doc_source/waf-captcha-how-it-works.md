# How AWS WAF CAPTCHA works<a name="waf-captcha-how-it-works"></a>

AWS WAF CAPTCHA is a standard rule action, so it's relatively easy to implement\. To use CAPTCHA, you create the inspection criteria for your rule that identifies the requests that you want to challenge, and then specify the rule action CAPTCHA\. For general information about rule action options, see [AWS WAF rule action](waf-rule-action.md)\.

**Topics**
+ [CAPTCHA tokens and token expiration](#waf-captcha-tokens)
+ [CAPTCHA action behavior](#waf-captcha-action)
+ [CAPTCHA actions in the logs and metrics](#waf-captcha-logs-metrics)

## CAPTCHA tokens and token expiration<a name="waf-captcha-tokens"></a>

AWS WAF CAPTCHA uses tokens to track successful responses to CAPTCHA challenges\. When a user solves a CAPTCHA challenge, AWS automatically generates and encrypts a CAPTCHA token and sends it to the client as a cookie\. Then, when the client sends requests, it includes the encrypted CAPTCHA token in the request\. As needed, AWS WAF automatically decrypts the token and verifies that it's a valid CAPTCHA token\. The full contents of CAPTCHA tokens and detailed information about the encryption process are not publicly available\. 

Tokens include the timestamp of the last successful response to a challenge\. After a user successfully solves a CAPTCHA challenge, the client requests aren't challenged again until a rule with CAPTCHA action determines that their token has expired\. 

**Token immunity time**  
AWS WAF calculates token expiration using the CAPTCHA immunity time configuration\. This is the length of time that the client is immune from receiving a new CAPTCHA challenge after they've successfully completed a challenge\. The default immunity time is 300 seconds\. Valid values range from 60 to 259,200 seconds, or three days\.

You can configure the CAPTCHA immunity time in a web ACL's CAPTCHA configuration and in the configuration for a rule's CAPTCHA action setting\. A rule level setting overrides the web ACL setting\. For a CAPTCHA rule inside a rule group, if you don't define the immunity time for the rule, it will inherit the CAPTCHA configuration from each web ACL where you use the rule group\.

You can use the web ACL and rule level immunity time settings to tune CAPTCHA behavior\. For example, you can configure a rule that controls access to highly sensitive data with a low immunity time, and use a higher immunity time for your other rules\. Solving a CAPTCHA challenge can degrade your customers' website experience\. Tuning your immunity time settings in your rules can help you mitigate the impact on customer experience while still providing the protections that you want\. 

For information about configuring the immunity time, see [Configuring the CAPTCHA immunity time](waf-captcha-configuring.md)\.

## CAPTCHA action behavior<a name="waf-captcha-action"></a>

When a web request matches the inspection criteria of a rule with CAPTCHA action, AWS WAF determines how to handle the request according to the state of its CAPTCHA token, the rule's CAPTCHA immunity time configuration, and whether the request can handle a CAPTCHA page\. 

AWS WAF applies the CAPTCHA action to a web request as follows:
+ **Valid CAPTCHA token** – AWS WAF applies any labels and request customizations that you've configured for the rule action, and then continues evaluating the request using the remaining rules in the web ACL\. 
+ **Missing, invalid, or expired CAPTCHA token** – AWS WAF discontinues the web ACL evaluation of the request and blocks it from going to its intended destination\. 

  AWS WAF generates a response that it sends back to the client, which includes the following:
  + The header `x-amzn-waf-action` with a value of `captcha`\.
  + The HTTP status code `405 Method Not Allowed`\.
  + If the request contains an `Accept` header with a value of `text/html`, the response includes a CAPTCHA challenge\.

  AWS WAF only includes a challenge in the response if the request contains an `Accept` header with a value of `text/html`\. The CAPTCHA challenge is designed to be handled as HTML content, and it can only be handled properly by a client that's expecting HTML content\. 

  It's possible for a client to accept HTML but still not be able to handle an AWS WAF CAPTCHA challenge\. For example, a widget on a webpage with a small iFrame might accept HTML, but not be able to display the challenge or process it\. 

## CAPTCHA actions in the logs and metrics<a name="waf-captcha-logs-metrics"></a>

The CAPTCHA action can be a non\-terminating action, like Count, or a terminating action, like Block or Allow\. 
+ **Valid CAPTCHA token** – When the action finds a valid token and doesn't block the request, AWS WAF captures metrics and logs as follows:
  + Increments the metrics for `CaptchaRequests` and for `RequestsWithValidCaptchaToken`\. 
  + Logs the match as a `nonTerminatingMatchingRules` entry with action of CAPTCHA\. The following listing shows the section of a log for this type of match\.

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
+ **Missing, invalid, or expired CAPTCHA token** – When the action blocks the request due to a missing or invalid token, AWS WAF captures metrics and logs as follows:
  + Increments the metric for `CaptchaRequests`\. 
  + Logs the match as a `CaptchaResponse` entry with HTTP `405` status code\. The log indicates whether the request was missing the CAPTCHA token or had an expired token\. The log also indicates whether AWS WAF sent a CAPTCHA challenge page to the client\. The following listing shows the sections of a log for this type of match\.

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