# How to use the `fetch` wrapper<a name="waf-javascript-sdk-fetch-wrapper"></a>

You can use the `fetch` wrapper by changing your normal `fetch` calls to the `fetch` API under the `AwsWafIntegration` namespace\. The AWS WAF wrapper supports all of the same options as the standard JavaScript `fetch` API call\. This approach is generally the simplest way to integrate your application\. 

**Before the wrapper implementation**  
The following example listing shows standard code before implementing the `AwsWafIntegration` `fetch` wrapper\.

```
const login_response = await fetch(login_url, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: login_body
  });
```

**After the wrapper implementation**  
The following listing shows the same code with the `AwsWafIntegration` `fetch` wrapper implementation\.

```
const login_response = await AwsWafIntegration.fetch(login_url, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: login_body
  });
```