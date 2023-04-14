# Token characteristics<a name="waf-tokens-details"></a>

Each token has the following characteristics: 
+ The token is stored in a cookie named `aws-waf-token`\.
+ The token is encrypted\.
+ The token fingerprints the client session with a sticky granular identifier that contains the following information: 
  + The timestamp of the client's latest successful response to a silent challenge\. 
  + The timestamp of the end user's latest successful response to a CAPTCHA\. This is only present if you use CAPTCHA in your protections\. 
  + Additional information about the client and client behavior that can help separate your legitimate clients from unwanted traffic\. The information includes various client identifiers and client\-side signals that can be used to detect automated activities\. The information gathered is non\-unique and can't be mapped to an individual human being\. 

For security reasons, AWS doesn't provide a complete description of the contents of AWS WAF tokens or detailed information about the token encryption process\. 