# AWS WAF mobile SDK<a name="waf-mobile-sdk"></a>

You can use the AWS WAF mobile SDKs to implement AWS WAF application integrations for Android and iOS mobile applications\. With the mobile SDK, you can manage token authorization, and include the tokens in the requests that you send to your protected resources\. By using the SDK, you ensure that these remote procedure calls by your client contain a valid token\. Additionally, when this integration is in place on your application's pages, you can implement mitigating rules in your web ACL, such as blocking requests that don't contain a valid token\.

For access to the mobile SDKs, contact sales at [Contact AWS](http://aws.amazon.com/contact-us)\.

The basic approach for using the SDK is to create a token provider using a configuration object, then to use the token provider to retrieve tokens from the AWS token service\. By default, the token provider includes the retrieved tokens in your web requests to your protected resource\. 

The following is a partial listing of an SDK implementation, which shows the main components\. For more detailed examples, see [Writing your code for the AWS WAF mobile SDK](waf-mobile-sdk-coding-examples.md)\.

------
#### [ iOS ]

```
let url: URL = URL(string: "Web ACL integration URL")!
let configuration = WAFConfiguration(applicationIntegrationUrl: url, domainName: "Domain name")
let tokenProvider = WAFTokenProvider(configuration)
let token = tokenProvider.getToken()
```

------
#### [ Android ]

```
URL applicationIntegrationURL = new URL("Web ACL integration URL");
String domainName = "Domain name";
WAFConfiguration configuration = WAFConfiguration.builder().applicationIntegrationURL(applicationIntegrationURL).domainName(domainName).build();
WAFTokenProvider tokenProvider = new WAFTokenProvider(Application context, configuration);
WAFToken token = tokenProvider.getToken();
```

------