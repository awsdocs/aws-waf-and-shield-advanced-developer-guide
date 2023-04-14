# Writing your code for the AWS WAF mobile SDK<a name="waf-mobile-sdk-coding-examples"></a>

This section provides code examples for using the mobile SDK\. 

## Initializing the token provider and getting tokens<a name="waf-mobile-sdk-coding-basic"></a>

You initiate your token provider instance using a configuration object\. Then you can retrieve tokens using the available operations\. The following shows the basic components of the required code\.

------
#### [ iOS ]

```
let url: URL = URL(string: "Web ACL integration URL")!
let configuration = WAFConfiguration(applicationIntegrationUrl: url, domainName: "Domain name")
let tokenProvider = WAFTokenProvider(configuration)

//onTokenReady can be add as an observer for UIApplication.willEnterForegroundNotification
self.tokenProvider.onTokenReady() { token, error in
if let token = token {
//token available
}

if let error = error {
//error occurred after exhausting all retries
}
}

//getToken()
let token = tokenProvider.getToken()
```

------
#### [ Android ]

```
String applicationIntegrationURL = "Web ACL integration URL";
Or
URL applicationIntegrationURL = new URL("Web ACL integration URL");

String domainName = "Domain name";

WAFConfiguration configuration = WAFConfiguration.builder().applicationIntegrationURL(applicationIntegrationURL).domainName(domainName).build();
WAFTokenProvider tokenProvider = new WAFTokenProvider(Application context, configuration);

// implement a token result callback
WAFTokenResultCallback callback = (wafToken, error) -> {
  if (wafToken != null) {
    // token available
  } else {  
    // error occurred in token refresh  
  }
};

// Add this callback to application creation or activity creation where token will be used
tokenProvider.onTokenReady(callback);

// Once you have token in token result callback
// if background refresh is enabled you can call getToken() from same tokenprovider object
// if background refresh is disabled you can directly call getToken()(blocking call) for new token
WAFToken token = tokenProvider.getToken();
```

------

## Allowing the SDK to provide the token cookie in your HTTP requests<a name="waf-mobile-sdk-coding-auto-token-cookie"></a>

If `setTokenCookie` is `TRUE`, the token provider includes the token cookie for you in your web requests to all locations under the path that's specified in `tokenCookiePath`\. By default,`setTokenCookie` is `TRUE` and `tokenCookiePath` is `/`\. 

You can narrow the scope of the requests that include a token cookie by specifying the token cookie path, for example, `/web/login`\. If you do this, check that your AWS WAF rules don't inspect for tokens in the requests that you send to other paths\. When you use the `AWSManagedRulesATPRuleSet` rule group, you configure the login path, and the rule group checks for tokens in requests that are sent to that path\. For more information, see [Adding the ATP managed rule group to your web ACL](waf-atp-rg-using.md)\.

------
#### [ iOS ]

When `setTokenCookie` is `TRUE`, the token provider stores the AWS WAF token in a `HTTPCookieStorage.shared` and automatically includes the cookie in requests to the domain that you specified in `WAFConfiguration`\.

```
let request = URLRequest(url: URL(string: domainEndpointUrl)!)
//The token cookie is set automatically as cookie header
let task = URLSession.shared.dataTask(with: request) { data, urlResponse, error  in
}.resume()
```

------
#### [ Android ]

When `setTokenCookie` is `TRUE`, the token provider stores the AWS WAF token in a `CookieHandler` instance that's shared application wide\. The token provider automatically includes the cookie in requests to the domain that you specified in `WAFConfiguration`\.

```
URL url = new URL("Domain name");
//The token cookie is set automatically as cookie header
HttpsURLConnection connection = (HttpsURLConnection) url.openConnection();
connection.getResponseCode();
```

If you already have the `CookieHandler` default instance initialized, the token provider will use it to manage cookies\. If not, the token provider will initialize a new `CookieManager` instance with the AWS WAF token and `CookiePolicy.ACCEPT_ORIGINAL_SERVER` and then set this new instance as the default instance in `CookieHandler`\.

The following code shows how the SDK initializes the cookie manager and cookie handler when they aren't available in your app\. 

```
CookieManager cookieManager = (CookieManager) CookieHandler.getDefault();
if (cookieManager == null) {
    // Cookie manager is initialized with CookiePolicy.ACCEPT_ORIGINAL_SERVER
    cookieManager = new CookieManager();
    CookieHandler.setDefault(cookieManager);
}
```

------

## Manually providing the token cookie in your HTTP requests<a name="waf-mobile-sdk-coding-manual-token-cookie"></a>

If you set `setTokenCookie` to `FALSE`, then you need to provide the token cookie manually, as a Cookie HTTP request header, in your requests to your protected endpoint\. The following code shows how to do this\.

------
#### [ iOS ]

```
var request = URLRequest(url: wafProtectedEndpoint)
request.setValue("aws-waf-token=token from token provider", forHTTPHeaderField: "Cookie")
request.httpShouldHandleCookies = true
URLSession.shared.dataTask(with: request) { data, response, error in }
```

------
#### [ Android ]

```
URL url = new URL("Domain name");
HttpsURLConnection connection = (HttpsURLConnection) url.openConnection();
String wafTokenCookie = "aws-waf-token=token from token provider";
connection.setRequestProperty("Cookie", wafTokenCookie);
connection.getInputStream();
```

------