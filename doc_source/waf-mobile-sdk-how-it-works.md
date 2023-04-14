# How the AWS WAF mobile SDK works<a name="waf-mobile-sdk-how-it-works"></a>

The mobile SDKs provide you with a configurable token provider that you can use for token retrieval and use\. The token provider verifies that the requests that you allow are from legitimate customers\. When you send requests to the AWS resources that you protect with AWS WAF, you include the token in a cookie, to validate the request\. You can handle the token cookie manually or have the token provider do it for you\.

This section covers the interactions between the classes, properties, and methods that are included in the mobile SDK\. For the SDK specification, see [The AWS WAF mobile SDK specification](waf-mobile-sdk-specification.md)\. 

## Token retrieval and caching<a name="waf-mobile-sdk-how-token-basics"></a>

When you create the token provider instance in your mobile app, you configure how you want it to manage tokens and token retrieval\. Your main choice is how to maintain valid, unexpired tokens for use in your app’s web requests:
+ **Background refresh enabled** – This is the default\. The token provider automatically refreshes the token in the background and caches it\. With background refresh enabled, when you call `getToken()`, the operation retrieves the cached token\. 

  The token provider performs the token refresh at configurable intervals, so that an unexpired token is always available in the cache while the application is active\. Background refresh is paused while your application is in an inactive state\. For information about this, see [Retrieving a token following app inactivity](#waf-mobile-sdk-how-back-from-inactive)\.
+ **Background refresh disabled** – You can disable background token refresh, and then retrieve tokens only on demand\. Tokens retrieved on demand aren't cached, and you can retrieve more than one if you want\. Each token is independent of any others that you retrieve, and each has its own timestamp that's used to calculate expiration\.

  You have the following choices for token retrieval when background refresh is disabled: 
  + **`getToken()`** – When you call `getToken()` with background refresh disabled, the call synchronously retrieves a new token from AWS WAF\. This is a potentially blocking call that may affect app responsiveness if you invoke it on the main thread\. 
  + **`onTokenReady(WAFTokenResultCallback)`** – This call asynchronously retrieves a new token and then invokes the provided result callback in a background thread when a token is ready\. 

### How the token provider retries failed token retrievals<a name="waf-mobile-sdk-how-token-retrieval-retries"></a>

The token provider automatically retries token retrieval when retrieval fails\. Retries are initially performed using exponential backoff with a starting retry wait time of 100 ms\. For information about exponential retries, see [Error retries and exponential backoff in AWS](https://docs.aws.amazon.com/general/latest/gr/api-retries.html)\.

When the number of retries reaches the configured `maxRetryCount`, the token provider either stops trying or switches to trying every `maxErrorTokenRefreshDelayMsec` milliseconds, depending on the type of token retrieval: 
+ **`onTokenReady()`** – The token provider switches to waiting `maxErrorTokenRefreshDelayMsec` milliseconds between attempts, and continues trying to retrieve the token\. 
+ **Background refresh** – The token provider switches to waiting `maxErrorTokenRefreshDelayMsec` milliseconds between attempts, and continues trying to retrieve the token\. 
+ **On\-demand `getToken()` calls, when background refresh is disabled** – The token provider stops trying to retrieve a token and returns the previous token value, or a null value if there is no previous token\. 

## Retrieving a token following app inactivity<a name="waf-mobile-sdk-how-back-from-inactive"></a>

Background refresh is only performed while your app is considered active for your app type: 
+ **iOS** – Background refresh is performed when the app is in the foreground\.
+ **Android** – Background refresh is performed when the app isn't closed, whether it's in the foreground or background\.

If your app remains in any state that doesn’t support background refresh for longer than your configured `tokenRefreshDelaySec` seconds, the token provider pauses background refresh\. For example, for an iOS app, if `tokenRefreshDelaySec` is 300 and the app closes or goes into the background for more than 300 seconds, the token provider stops refreshing the token\. When the app returns to an active state, the token provider automatically restarts background refresh\. 

When your app comes back to an active state, call `onTokenReady()` so you can be notified when the token provider has retrieved and cached a new token\. Don't just call `getToken()`, because the cache may not yet contain a current, valid token\. 