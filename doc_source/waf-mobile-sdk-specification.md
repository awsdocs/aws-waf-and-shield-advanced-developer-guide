# The AWS WAF mobile SDK specification<a name="waf-mobile-sdk-specification"></a>

This section lists the SDK objects, operations, and configuration settings for the AWS WAF mobile SDK\. For detailed information about how the token provider and operations work for the various combinations of configuration settings, see [How the AWS WAF mobile SDK works](waf-mobile-sdk-how-it-works.md)\. 

**`WAFToken`**  
Holds an AWS WAF token\.    
**`getValue()`**  
Retrieves the `String` representation of the `WAFToken`\. 

**`WAFTokenProvider`**  
Manages tokens in your mobile app\. Implement this using a `WAFConfiguration` object\.    
**`getToken()`**  
If background refresh is enabled, this returns the cached token\. If background refresh is disabled, this makes a synchronous, blocking call to AWS WAF to retrieve a new token\.   
**`onTokenReady(WAFTokenResultCallback)`**  
Instructs the token provider to refresh the token and invoke the provided callback when an active token is ready\. The token provider will invoke your callback in a background thread when the token is cached and ready\. Call this when your app first loads and also when it comes back to an active state\. For more information about returning to an active state, see [Retrieving a token following app inactivity](waf-mobile-sdk-how-it-works.md#waf-mobile-sdk-how-back-from-inactive)\.   
For Android or iOS apps, you can set `WAFTokenResultCallback` to the operation that you want the token provider to invoke when a requested token is ready\. Your implementation of `WAFTokenResultCallback` must take the parameters `WAFToken`, `SdkError`\. For iOS apps, you can alternately create an inline function\. 

**`WAFConfiguration`**  
Holds the configuration for the implementation of the `WAFTokenProvider`\. When you implement this, you provide your web ACL’s integration URL, the domain name to use in the token, and any non\-default settings that you want the token provider to use\.   
The following list specifies the configuration settings that you can manage in the `WAFConfiguration` object\.    
**`applicationIntegrationUrl`**   
The application integration URL\. Get this from the AWS WAF console or through the `getWebACL` API call\.  
Required: Yes  
Type: App\-specific URL\. For iOS, see [iOS URL](https://developer.apple.com/documentation/foundation/url)\. For Android, see [java\.net URL](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html)\.   
**`backgroundRefreshEnabled`**   
Indicates whether you want the token provider to refresh the token in the background\. If you set this, the token provider refreshes your tokens in the background according to the configuration settings that govern automatic token refresh activities\.   
Required: No  
Type: `Boolean`  
Default value: `TRUE`  
**`domainName`**   
The domain to use in the token, which is used in token acquisition and cookie storage\. For example, `example.com` or `aws.amazon.com`\. This is usually the host domain of your resource that’s associated with the web ACL, where you’ll be sending web requests\. For the `AWSManagedRulesATPRuleSet` managed rule group, this will usually be a single domain that matches the domain in the login path that you provided to the rule group configuration\.   
Public suffixes aren't allowed\. For example, you can't use `usa.gov` or `co.uk` as the token domain\.  
The domain must be one that AWS WAF will accept, based on the protected host domain and the web ACL's token domain list\. For more information, see [Configuring the web ACL token domain list](waf-tokens-domains.md#waf-tokens-domain-lists)\.  
Required: Yes  
Type: `String`   
**`maxErrorTokenRefreshDelayMsec`**   
The maximum time in milliseconds to wait before repeating a token refresh after a failed attempt\. This value is used after token retrieval has failed and been retried `maxRetryCount` times\.   
Required: No  
Type: `Integer`  
Default value: `5000` \(5 seconds\)  
Minimum value allowed: `1` \(1 millisecond\)  
Maximum value allowed: `30000` \(30 seconds\)  
**`maxRetryCount`**   
The maximum number of retries to perform with exponential backoff when a token is requested\.   
Required: No  
Type: `Integer`  
Default value: If background refresh is enabled, `5`\. Otherwise, `3`\.  
Minimum value allowed: `0`  
Maximum value allowed: `10`  
**`setTokenCookie`**   
Indicates whether you want the SDK’s cookie manager to add a token cookie in your requests\. By default, this adds a token cookie to all requests\. The cookie manager adds a token cookie to any request whose path is under the path specified in `tokenCookiePath`\.   
Required: No  
Type: `Boolean`  
Default value: `TRUE`  
**`tokenCookiePath`**   
Used when `setTokenCookie` is `TRUE`\. Indicates the top\-level path where you want the SDK’s cookie manager to add a token cookie\. The manager adds a token cookie to all requests that you send to this path and to all child paths\.   
For example, if you set this to `/web/login`, then the manager includes the token cookie for everything sent to `/web/login` and any of its child paths, like `/web/login/help`\. It doesn't include the token for requests sent to other paths, like `/`, `/web`, or `/web/order`\.   
Required: No  
Type: `String`  
Default value: `/`  
**`tokenRefreshDelaySec`**   
Used for background refresh\. The maximum amount of time in seconds between background token refreshes\.  
Required: No  
Type: `Integer`  
Default value: `300` \(5 minutes\)  
Minimum value allowed: `300` \(5 minutes\)  
Maximum value allowed: `600` \(10 minutes\)